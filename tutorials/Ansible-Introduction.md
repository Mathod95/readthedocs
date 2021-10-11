<p align="center">
  <img src="https://cdn.icon-icons.com/icons2/2699/PNG/512/ansible_logo_icon_169596.png">
</p>

[Ansible] outil incontournable de gestion d’infrastructure ayant pour target principale les systemes Linux. Il est capable de représenter la gestion de la configuration d’une infrastructure sous forme de code, aisé à lire et à gérer. 

[Ansible]: https://www.redhat.com/fr/technologies/management/ansible

# Prérequis
Pour aborder ce document quelques pré-requis sont nécessaires :
- Avoir les notions de base en administration Linux de base (Utilisateurs, fichiers, services, réseau, stockage, système de fichiers, pare-feu, Selinux, etc.)
- Maîtriser un éditeur de texte comme vim
- Maîtriser un SCM comme git
- Avoir des notions de virtualisation logicielle et/ou matérielle

# Objectif atteints grace à Ansible
- Le minimum par nature. Les systèmes de gestion ne devraient pas imposer des dépendances supplémentaires sur l’environnement.
- La cohérence. cf. notion de test unitaire (procédure permettant de vérifier le bon fonctionnement d’une partie précise d’un logiciel ou d’une portion d’un programme).
- La sécurité. Ansible ne déploie pas des agents sur les noeuds. Un protocole de transport comme OpenSSH ou HTTPS est seulement nécessaire pour commencer une gestion.
- La fiabilité. Lorsqu’il est écrit soigneusement, un livre de jeu Ansible peut être idempotent afin d’éviter des effets secondaires inattendus sur les systèmes gérés.
- Une courbe d’apprentissage faible. Les livres de jeux Ansible utilisent un langage simple et descriptif basé sur YAML et les modèles Jinja2.

# Présentation de ce document

En guise d’introduction, on décrira dans ce document le projet Ansible, ses cas d’usage, ses composants, son principe de fonctionnement, son installation et les différents binaires qui l’accompagnent.

Après des généralités, le document décrit la terminologie et les composants Ansible. Il indique les procédures d’installation de Ansible sur une machine `ControlNode` Debian.

On tentera ici de comprendre de manière sommaire les composants de base d’Ansible tels que les connexions selon les cibles, les inventaires, les modules, les collections, le mode ad-hoc, les variables, les “Facts”, les playbooks, les fichiers de configuration YAML, les sorties JSON et les modèles Jinja2, les rôles, Ansible AWX, l’idempotence.

Enfin, on ne manquera de décrire l’environnement d’exécution d’Ansible en décrivant les différentes commandes ansible disponibles nativement.

# Présentation générale

Ansible est un outil open-source de provisionnement de logiciels, de gestion des configurations et de déploiement d’applications qui permet de faire de l’IaC. Il fonctionne sur de nombreux systèmes de type Unix et peut configurer aussi bien des systèmes Microsoft Windows. Il comprend son propre langage **déclaratif** pour décrire la configuration du système. Ansible est agent-less, se connectant temporairement à distance via SSH ou Windows Remote Management (permettant l’exécution à distance de PowerShell) pour effectuer ses tâches.

Ansible gère les différents noeuds avec un accès à distance natif (tels que les protocoles SSH ou Remote PowerShell ou encore des APIs natives). Il ne nécessite l’installation d’aucun logiciel supplémentaire à distance. Il offre des capacités de parallélisation, collecte de métadonnées et gestion des états. Cet aspect de conception “sans agent” installé sur le périphérique est important car il réduit les besoins d’infrastructure pour démarrer une gestion. Les modules fonctionnent grâce à JSON et à la sortie standard et peuvent être écrits dans n’importe quel langage de programmation.Le système utilise notamment YAML pour exprimer des descriptions réutilisables de systèmes, il fournit des sorties en JSON, il traite les variables grâce à des modèles Jinja2.

Le logiciel Ansible a été conçu par un ancien employé Red Hat, Michael DeHaan, également auteur de l’application de serveur de “provisionning” Cobbler et co-auteur du framework Func pour l’administration à distance. Le code source du logiciel est sous licence GNU General Public v3.0. Red Hat a racheté la société Ansible, Inc. en octobre 2015[¹].

[¹]: https://docs.ansible.com/ansible/latest/user_guide/modules.html

# Version d’Ansible

Jusqu’à la version 2.9.*, le code source Ansible était situé dans un seul projet [ansible/ansible] avec deux mises à jour principales par an.

Ansible Classique (jusqu’en version 2.9) se caractérisait par :
- Un dépôt unique ansible/ansible.
- Un paquet unique appelé ansible
- Des major release deux fois par an

La version 2.10 (Ansible 3) de Ansible va fondamentalement changer la portée des plugins inclus dans le dépôt [ansible/ansible], en déplaçant une grande partie des plugins dans des dépôts de [collections](https://github.com/ansible-collections) plus petits et qui seront distribués via https://galaxy.ansible.com/.

Après la version 2.10, qui a marqué le changement de packaging de Ansible, voici la version 2.11 (Ansible 4) Comme annoncé, elle est basé sur le package ansible-core (Précedement ansible-base pour Ansible 3/2.10) 2.11 et contient toute une série de mise à jour sur les collections incluses. Vous pouvez retrouver la liste complète ici : [CHANGELOG-v4](https://github.com/ansible-community/ansible-build-data/blob/main/4/CHANGELOG-v4.rst#release-summary)

>Pour obtenir le numéro de la dernière version stable de Ansible :
>```
>curl -s https://pypi.org/pypi/ansible-core/json | jq -r '.releases | keys | sort'
>```
> [Project Page Pypi](https://pypi.org/project/ansible/)

[ansible/ansible]: https://www.redhat.com/fr/engage/delivery-with-ansible-20170906?sc_cid=7013a000002w14HAAQ&gclid=CjwKCAjw49qKBhAoEiwAHQVTo8TN7CpckbukpAnsE5vo0I4Eezh8EWbISPcNgHhxZn_ChU7kMOYvvRoCgP0QAvD_BwE&gclsrc=aw.ds

# Release cycle et maintenance

Aussi depuis la version 2.10. la version majeure est maintenue pendant un cycle de publication. Lorsque la version suivante sort (Dans notre cas 2.11), la version plus ancienne (2.10 dans cet exemple) n’est plus maintenue.

Concrètement, le dépôt ansible/ansible (ansible-base) ne contient plus que :

- Les programmes de base Ansible, `ansible-{playbook,galaxy,doc,test,etc}`.
- Quelques documents.
- Un minuscule sous-ensemble de modules et de plugins pour permettre le fonctionnement d’un ControlNode.

Tous ces éléments seront connus sous le nom d’**ansible-core**.

[Release cycle overview](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html#release-cycle-overview)

# Integration
Ansible s'intègre facilement à avec du matériel, du logiciel ou des solutions d’un grand nombre de fournisseurs du domaine des infrastructures comme :

- Source Control Mgmt: GitHub, Bitbucket, Gitlab, ...
- Continuous Integration: Jenkins, TeamCity, Travic CI, ...
- Testing: JMeter, Selenium, ...
- Containers: Docker, ECS, GKE, ...
- Cloud: AWS, Azure, GCP, ...
- AIOps: Splunk, Logstash, Prometheus, ...
- Analytics: Kibana, DataDog, ElasticSearch, ...
- Monitoring: Zabbix, Nagios, ...
- Collaboration: Slack, Jira, Trello, ...
- ...

[Official Integration list]:https://docs.ansible.com/ansible/latest/collections/community/general/index.html

# Automatiser et coder l’infrastructure
Nous allons progressivement apprendre que manipuler Ansible consiste à écrire du texte géré sous forme de code. L’ambition est donc de "coder l’infrastructure". Alors comment coder l’infrastructure ? D’un point de vue historique, pour un parc de machines Linux, on commencera avec du Bash, ensuite probablement du Perl, et sans doute du Python. Or le personnel d’infrastructure s’il a choisi cette voie dans les métiers de l’informatique dipose de peu d’appétence pour une pratique de "développeur" d’autant plus que l’apprentissage d’un langage de programmation classique exigera une longue courbe d’apprentissage pour cetains profils.

Or Ansible permettra au personnel informatique d’automatiser les infrastructures. Il a l’avantage d’être :

- Populaire, diposant d’une communauté large.
- Flexible, sans limite sur les fonctions ou les cibles à gérer.
- Evolutif, aisé à adapter (en Python ou autres).
- Lisible par tous et à courbe d’apprentissage faible, grâce au format YAML.

Le seul écueil est de connaître les solutions à gérer à travers cet outil de telle sorte qu’une maîtrise d’une solution Ansible passe aussi par une bonne maîtrise de ce qui est déployé par Ansible.

Il faut alors voir Ansible comme une surcouche sans état (mis en intermédiaire qui fonctionne de manière très simple) qui intègre d’autres solutions ou s’intègre à d’autres facilement. Ansible Tower et son fork OpenSource AWX renforcent cette capacité de manière crédible en ajoutant des fonctions de gestion des utilisateurs, du code et des secrets.

# Diagrammes de fonctionnement de Ansible Composants d'Ansible

![bg w:900](https://d33wubrfki0l68.cloudfront.net/a164b363e34dda928909d730081a7dc574f07155/90a4d/assets/images/ansible/linklight/how-ansible-works-diagram-01.svg.png)

- Users: Users who create Ansible playbook has a direct connection with ansible automation Engine.
- Ansible playbook: It also interacts with the ansible automation engine and configuration Management Database
- Public or Private cloud: They help in interacting with all the modules and API with this but also with the entire cloud which proves that it has security measures as well.
- Inventory: Inventory which is a part of the automation engine helps in provisioning and internal provisioning using automation.
- API: It helps in creating necessary API for the interaction of end to end modules.
- Modules: The modules are directly run using playbooks the modules can control all services, packages, AWS cloud formation, etc.
- Plugins: All necessary cache, logging purpose, ansibles functioning all help in creating augmented ansible’s core.
- Networking: It helps to automate different networks that make use of all agentless frames and generate useful configurations.
- Hosts: Hosts here refers to the machines like Linux or Unix machines which are getting automated using Ansible.
- CMDB (Configuration Management Database): It is a kind of repository that consists of an entire network of computers of operational or IT infrastructure.

## Ansible Automation Engine
En vue de contrôler des noeuds distants, des utilisateurs lancent des "playbooks" à partir d’un ControlNode grâce à Ansible Engine.

Ansible Engine utilise différents composants comme :

- Des modules
- Des plugins
- Une API
- Un inventaire

---

Control Node:
La machine de contrôle doit être un hôte Linux / Unix (par exemple, Red Hat Enterprise Linux, Debian, CentOS, OS X, BSD, Ubuntu), et Python 2.7 ou Python 3.5+ sont requis. Avec une version Windows 10 Pro, il est possible d’utiliser Ansible avec WSL, voir Can Ansible run on Windows?

Managed Nodes:
- Les noeuds gérés, s’ils sont en Linux/Unix, doivent disposer de Python 3. SSH est alors le mode de connexion préféré.
- Ansible peut également gérer des noeuds Windows. Dans ce cas, on utilise PowerShell à distance de manière native au lieu de SSH.
- Le matériel d’infrastructure réseau (“constructeurs”), pare-feux, serveurs de stockage, fournisseurs IaaS, solutions de virtualisation sont supportés via SSH, NETCONF/YANG ou encore via des API HTTP REST.

---

![bg w:900](https://d33wubrfki0l68.cloudfront.net/0d369d7d07a6c678df31e6eebdd5985202dbfa57/8c1f8/assets/images/ansible/linklight/local_execution.svg.png)

---

SSH-Key
Le noeud de controle et les hosts devraient a priori simplement communiquer grâce au service SSH.

Les mots de passe sont pris en charge, mais la gestion des clés SSH avec ssh-agent est l’un des meilleurs moyens d’utiliser Ansible. Il est également possible d’utiliser parmi beaucoup de possibilités des authentifications Kerberos ou autres. Les connexions “root” ne sont pas obligatoires, on peut se connecter en tant qu’utilisateur, et puis utiliser “su” ou “sudo”. Le module “authorized_key” d’Ansible est un excellent moyen d’utiliser Ansible pour contrôler les accès SSH.

```
ssh-agent bash
ssh-add ~/.ssh/id_rsa
```

Notez que ssh-agent s’utilise avec des clés avec des passphrase.

On trouvera sous les liens un document de formation détaillé sur l’usage du protocole avec OpenSSH (Linux/Windows) et d’autres sur la configuration de Cisco IOS pour supporter des connexions SSH.

Ansible supporte beaucoup d’autres types de connexions/communications avec ses cîbles.

---

Installation via PIP
Sous Debian, l’installation de pip3 se fait à l’aide de la commande apt suivie de l’option install et du nom du package python-pip3 :

```
sudo apt install python3 python-pip3
```

Une fois pip installé, il est possible de lancer l’installation d’Ansible avec la commande suivante :

```
sudo pip3 install ansible
```

Dans le cas où vous auriez déjà une version installée que vous voudriez mettre à jour, il faudra ajouter l’option --upgrade :

```
sudo pip3 install --upgrade ansible
```

---

Vérification de la version d’Ansible
Pour vérifier la version d'Ansible nous allons utiliser la commande suivante :

```
evina@ANSIBLE:~$ ansible --version
ansible 2.10.4
  config file = None
  configured module search path = ['/home/evina/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.7/dist-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 3.7.3 (default, Jul 25 2020, 13:03:44) [GCC 8.3.0]
```

---

NETWORK TIME
```
sudo apt remove ntp
sudo vim /etc/systemd/timesyncd.conf (uncomment NTP)
timedatectl set-ntp true
sudo systemctl restart systemd-timesyncd.service
systemctl status systemd-timesyncd.service
```

---

Contexte et prérequis
Les point que vous allez travailler et mettre en œuvre : 
Installation d'Ansible via Python pip3
Connaissance & prérequis nécessaire : 
Installation de package sous Debian 10
Matériel à disposition : 
Serveur Debian 10
Connaissance acquise à la fin de ce chapitre : 
Installation de Ansible sous Debian 10

---





































# Key components:

- Node Mannager: ou control node, est le poste depuis lequel tout est executé via des connexions, essentiellement en SSH, aux nodes de l’inventaire. à sa connexion SSH.
- Playbook: Un playbook Ansible est une séquence de tâches ou de rôles décrits dans un fichier ou format yaml.
- Inventory: La liste des systèmes cibles gérés par Ansible est appelé un inventaire. On distingue deux type d’inventaire : l’inventaire statique constitué d’un fichier décrivant la hiérarchie des serveurs et l’inventaire dynamique fourni par un système centralisé recensant tous les nodes de l’infrastructure (ex NoCMDB)
- Module:Les tâches et les rôles font appel à des modules mis à disposition avec Ansible. Je vous invite à consulter la liste sur le site d’Ansible.
- Template: Comme son nom l’indique, un template est un modèle permettant de générer un fichier cible. Ansible utilise Jinja2, un gestionnaire de modèles écrit pour Python. Les « Templates » Jinja2 permettent de gérer des boucles, des tests logiques, des listes ou des variable.
- Notifier: indique que si une tâche change d’état (et uniquement si la tâche a engendré un changement), notify fait appel au handler associé exécuter une autre tâche.
- Handler: Tâche qui n’est appelée que si un notifier est invoqué
- Tag: Nom défini sur une ou plusieurs tâche qui peut être utilisé plus tard pour exécuter uniquement ce ou ces tâches Ansible.
- Rôle: Afin d’éviter d’écrire encore et encore les mêmes playbooks, les roles Ansible apportent la possibilité de regrouper des fonctionnalités spécifiques dans ce qu’on appelle des rôles. Il seront ensuite intégrés aux playbooks Ansible.

# Notion de base d’Ansible
## Les principales commandes Ansible
Ansible est livré avec un certain nombre de commandes permettant de soit lancer des actions ou soit obtenir de l’information sur l’environnement d’execution Ansible :

- ansible : Permet d'exécuter un simple module ansible sur un inventaire. Vu ci-dessus dans le premier test.
- ansible-console : Ouvre une console interactive permettant de lancer plusieurs actions sur un inventaire.
- ansible-config : Affiche l’ensemble des paramètres Ansible. ansible-config [list|dump|view].
  - list : affiche la liste complète des options d’Ansible à disposition.
  - dump : affiche la configuration dans le contexte actuel.
  - view : affiche le contenu d’un fichier de configuration Ansible
- ansible-playbook : Exécute un playbook Ansible sur un inventaire. La plus connue.
- ansible-vault : Permet de crypter des données qui ne doivent être divulgué.
- ansible-inventory : Affiche l’ensemble des données d’un inventaire Ansible.
- ansible-galaxy : permet d’installer des roles et des collections Ansible
- ansible-doc : Permet de lister l’ensemble des composants Ansible à disposition sur le noeud d’execution ansible-doc -l -t [type] type parmi: become, cache, callback, cliconf, connection,httpapi, inventory, lookup, netconf, shell, vars, module, strategy.


# Installing Ansible on Debian 11
Debian users may use the same source as the Ubuntu PPA (using the following table).

Debian | Ubuntu
------ | ------
Debian 11 (Bullseye) | Ubuntu 20.04 (Focal)
Debian 10 (Buster) | Ubuntu 18.04 (Bionic)

Add the following line to /etc/apt/sources.list.d/ansible.list:

```
echo -e "deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main" | sudo tee -a /etc/apt/sources.list.d/ansible.list
```

Then run these commands:

```
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
$ sudo apt update
$ sudo apt install ansible
```

Finally run `ansible --version` to confirm the installation:

```
mathod@MATHOD:~$ sudo ansible --version
ansible [core 2.11.5]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]
  jinja version = 2.11.3
  libyaml = True
```

[Official documentation - Installating Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

---

# Usefull links

## Ansible
- [Introduction à Ansible](https://blog.stephane-robert.info/post/introduction-ansible/) - Stéphane Robert

## Ansible Console
- [Ansible-Console introduction](https://blog.stephane-robert.info/post/ansible-console/) - Stéphane Robert

## Jinja
- [Jinja introduction](https://blog.stephane-robert.info/post/ansible-template-jinja/) - Stéphane Robert

## Vault
- [Vault Introduction](https://blog.stephane-robert.info/post/ansible-vault/) - Stéphane Robert

## Block
- [Blocks introduction](https://blog.stephane-robert.info/post/ansible-blocks/) - Stéphane Robert

## Lookup
- [Create Lookup for Ansible](https://blog.stephane-robert.info/post/ansible-plugin-lookup/) -Stéphane Robert

## Collection
- [Introduction collections Ansible](https://blog.stephane-robert.info/post/ansible-collections/) - Stéphane Robert

## Playbook
- [Création, execution et debug Playbook](https://blog.stephane-robert.info/post/ecriture-de-playbooks-ansible/) - Stéphane Robert

## Kitchen-CI
- [Kitchen-CI + Ansible](https://blog.stephane-robert.info/post/test-role-ansible-kitchenci-serverspec/) - Stéphane Robert

## Inventory
- [Ansible Inventory](https://blog.stephane-robert.info/post/ansible-inventaire-static-precedence-tips/) - Stéphane Robert

## Gestion de tests
- [Gestion de test via TDD](https://blog.stephane-robert.info/post/ansible-test-infra-playbook/) - Stéphane Robert

## Patchnote
- [Ansible 3.0](https://blog.stephane-robert.info/post/ansible-3.0-nouveautes-changements/) - Stéphane Robert
- [Ansible 4.0](https://blog.stephane-robert.info/post/ansible-4.0/) - Stéphane Robert

## Filter
- [Filter and finder json data](https://blog.stephane-robert.info/post/ansible-filtres-advanced-2/) - Stéphane Robert
- [Create a filter](https://blog.stephane-robert.info/post/ansible-plugin-filters/) - Stéphane Robert
- [Filter and use data](https://blog.stephane-robert.info/post/ansible-filtres-advanced-3/) - Stéphane Robert

## Lint
- [Ansible Linter](https://blog.stephane-robert.info/post/ansible-check-lint/) - Stéphane Robert

## Modules
  - [APT module](https://blog.stephane-robert.info/post/ansible-module-package-apt-yum/) - Stéphane Robert
  - [LineInFile & BlockInFile module](https://blog.stephane-robert.info/post/ansible-module-lineinfile-blockinfile/) - Stéphane Robert
  - [Services module](https://blog.stephane-robert.info/post/ansible-module-service-service_facts/) - Stéphane Robert
---

## To identify
- https://blog.stephane-robert.info/post/ansible-filtres-advanced/ - Stéphane Robert
- https://blog.stephane-robert.info/post/ansible-piloter-vos-container/ - Stéphane Robert