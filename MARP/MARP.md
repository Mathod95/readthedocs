---
marp: true
_class: invert
---
<!-- paginate: true -->

### **Ansible** <!--fit-->

[Ansible] est devenu un outil incontournable de gestion d’infrastructure pour des cibles Linux mais aussi pour des cibles du réseau et du centre de données, du nuage. Il est capable de représenter la gestion de la configuration d’une infrastructure sous forme de code, aisé à lire et à gérer. Ansible transforme l’esprit de l’admin traditionnel en dev.

[Ansible]: https://www.redhat.com/fr/engage/delivery-with-ansible-20170906?sc_cid=7013a000002w14HAAQ&gclid=CjwKCAjw49qKBhAoEiwAHQVTo8TN7CpckbukpAnsE5vo0I4Eezh8EWbISPcNgHhxZn_ChU7kMOYvvRoCgP0QAvD_BwE&gclsrc=aw.ds

---

### Prérequis

Pour aborder cette matière quelques pré-requis sont nécessaires :

- Avoir les notions de base en administration Linux de base (Utilisateurs, fichiers, services, réseau, stockage, système de fichiers, pare-feu, Selinux, etc.)
- Maîtriser un éditeur de texte comme vim
- Maîtriser un SCM comme git
- Disposer des concepts de scripting Bash
- Avoir des notions de virtualisation logicielle et/ou matérielle

---

### Portée du document

Ce document a pour premier objectif de répondre aux sujets du programme de l’examen de certification RHCE EX294 (Ingénieur certifié Red Hat) pour Red Hat Enterprise Linux 8. Ceux-ci portent sur les compétences de base en administration d’un système Linux RHEL 8 à travers l’outil de gestion Ansible, en ce y compris la gestion du pare-feu, des services de base et de Selinux.

Toutefois, si Ansible est capable de gérer une infrastructure entière qui n’est probablement pas seulement composée de systèmes Red Hat, on ne manquera pas de développer d’autres objectifs comme :

- Une gestion des cibles système Debian/Ubuntu ou Microsoft Windows
- Une gestion des cibles du réseau en ne citant que Cisco IOS
- Une gestion des cibles dans le nuage en ne citant que AWS ou OpenStack
- Une gestion d’une cible populaire comme VMWare vCenter
en tant que wrapper d’API HTTP Rest

---

### Présentation du produit Ansible

En guise d’introduction, on décrira dans ce document le projet Ansible, ses cas d’usage, ses composants, son principe de fonctionnement, son installation et les différents binaires qui l’accompagnent.

Après des généralités, le document décrit la terminologie et les composants Ansible. Il indique les procédures d’installation de Ansible sur une machine de contrôle Red Hat, CentOS, Fedora, Debian, Ubuntu, via PIP ou encore sous Windows WSL.

On tentera ici de comprendre de manière sommaire les composants de base d’Ansible tels quele s connexions selon les cibles, les inventaires, les modules, les collections, le mode ad-hoc, les variables, les “Facts”, les jeux, les playbooks ou livres de jeux, les fichiers de configuration YAML et INI, les sorties JSON et les modèles Jinja2, les rôles, Ansible AWX, l’idempotence.

Enfin, on ne manquera de décrire l’environnement d’exécution d’Ansible en décrivant les différentes commandes ansible* disponibles nativement.

---

### **1. Projet Ansible** <!--fit-->

---

## **1.1. Présentation générale**

Ansible est un outil open-source de provisionnement de logiciels, de gestion des configurations et de déploiement d’applications qui permet de faire de l’IaC. Il fonctionne sur de nombreux systèmes de type Unix, et peut configurer aussi bien des systèmes de type Unix que Microsoft Windows. Il comprend son propre langage déclaratif pour décrire la configuration du système. Ansible est sans agent, se connectant temporairement à distance via SSH ou Windows Remote Management (permettant l’exécution à distance de PowerShell) pour effectuer ses tâches.

---

Ansible gère les différents noeuds avec un accès à distance natif (tels que les protocoles SSH ou Remote PowerShell ou encore des APIs natives). Il ne nécessite l’installation d’aucun logiciel supplémentaire à distance. Il offre des capacités de parallélisation, collecte de métadonnées et gestion des états. Cet aspect de conception “sans agent” installé sur le périphérique est important car il réduit les besoins d’infrastructure pour démarrer une gestion. Les modules fonctionnent grâce à JSON et à la sortie standard et peuvent être écrits dans n’importe quel langage de programmation.Le système utilise notamment YAML pour exprimer des descriptions réutilisables de systèmes, il fournit des sorties en JSON, il traite les variables grâce à des modèles Jinja2.

---

Le logiciel Ansible a été conçu par un ancien employé Red Hat, Michael DeHaan, également auteur de l’application de serveur de “provisionning” Cobbler et co-auteur du framework Func pour l’administration à distance. Le code source du logiciel est sous licence GNU General Public v3.0. Red Hat a racheté la société Ansible, Inc. en octobre 2015[¹].

[¹]: https://docs.ansible.com/ansible/latest/user_guide/modules.html

---

## **1.2. Le terme Ansible**

Une “ansible” est un dispositif théorique permettant de réaliser des communications à une vitesse supraluminique (supérieure à la vitesse de la lumière) imaginé en 1966 par Ursula K. Le Guin dans son roman de science-fiction, Le Monde de Rocannon. Elle en détaillera plus tard le concept dans Les Dépossédés (1974). L’idée est notamment reprise par d’autres auteurs de livres de science-fiction et des jeux vidéos, la communication étant basée sur l’état d’énergie réciproque de deux particules jumelles. Par ailleurs, Ansible est le titre d’un magazine anglo-saxon consacré à la science-fiction. Enfin, le terme “ansible” peut faire référence à un système de communication hyperspace instantané fictif[²].

[²]: https://github.com/ansible-collections/overview
---

## **1.3. Version d’Ansible**

Jusqu’à la version 2.9.*, le code source Ansible était situé dans un seul projet [ansible/ansible] avec deux mises à jour principales par an[³].

Pour obtenir le numéro de la dernière version stable d’Ansible :

```
curl -s https://pypi.org/pypi/ansible-base/json | jq -r '.releases | keys | sort'
```
Ansible Classique (jusqu’en version 2.9) se caractérisait par :

- Un dépôt unique ansible/ansible.
- Un paquet unique appelé ansible
- Des sorties importantes deux fois par an

La version 2.10 d’Ansible va fondamentalement changer la portée des plugins inclus dans le dépôt ansible/ansible, en déplaçant une grande partie des plugins dans des dépôts de “collection” plus petits et qui seront distribués via https://galaxy.ansible.com/.

[ansible/ansible]: https://www.redhat.com/fr/engage/delivery-with-ansible-20170906?sc_cid=7013a000002w14HAAQ&gclid=CjwKCAjw49qKBhAoEiwAHQVTo8TN7CpckbukpAnsE5vo0I4Eezh8EWbISPcNgHhxZn_ChU7kMOYvvRoCgP0QAvD_BwE&gclsrc=aw.ds

[³]: https://fr.wikipedia.org/wiki/Ansible_(logiciel)

---

Aussi depuis la version 2.10. la version majeure est maintenue pendant un cycle de publication. Lorsque la version suivante sort (par exemple, 2.11), la version plus ancienne (2.10 dans cet exemple) n’est plus maintenue.

Concrètement, le dépôt ansible/ansible (ansible-base) ne contient plus que :

- Les programmes de base Ansible, `ansible-{playbook,galaxy,doc,test,etc}`.
- Quelques documents.
- Un minuscule sous-ensemble de modules et de plugins pour permettre le fonctionnement d’un contrôleur.

Tous ces éléments seront connus sous le nom d’**ansible-base**.

---

Les autres modules et plugins ont été déplacés dans diverses “collections”.

Ainsi pour les “collections” :

- Elles peuvent être publiées indépendamment d’**ansible-base** et d’Ansible, selon un cycle ou une cadence de publication que le responsable de la collection préfère.
- Elles ont leur propre repo (GitHub, GitLab, etc.) avec un backlog dédié, c’est-à-dire plus de backlog partagé de lancement massif et de relations publiques.
- On pourrait continuer à effectuer des tests d’IC et, dans de nombreux cas, on peut les effectuer de manière plus approfondie.

Le paquet publié d’Ansible 2.10 va intégrer **ansible-base** et les diverses collections communautaires qui faisaient auparavant partie d’ansible/ansible.

Le paquet `ansible` (contiendra un sous-ensemble de collections) et dépend du nouveau paquet **ansible-base** (Ansible engine).

---

## **1.4. Objectifs de conception de Ansible**

Les objectifs de conception de Ansible comprennent[⁴]:

- Le minimum par nature. Les systèmes de gestion ne devraient pas imposer des dépendances supplémentaires sur l’environnement.
- La cohérence. cf. notion de test unitaire (procédure permettant de vérifier le bon fonctionnement d’une partie précise d’un logiciel ou d’une portion d’un programme).
- La sécurité. Ansible ne déploie pas des agents sur les noeuds. Un protocole de transport comme OpenSSH ou HTTPS est seulement nécessaire pour commencer une gestion.
- La fiabilité. Lorsqu’il est écrit soigneusement, un livre de jeu Ansible peut être idempotent afin d’éviter des effets secondaires inattendus sur les systèmes gérés.
- Une courbe d’apprentissage faible. Les livres de jeux Ansible utilisent un langage simple et descriptif basé sur YAML et les modèles Jinja2.

[⁴]: https://github.com/ansible/ansible/blob/devel/README.rst

--- 

### **2. Integration** <!--fit-->

---

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
- ...[⁵]

[⁵]:https://docs.w3cub.com/ansible~2.9/modules/list_of_cloud_modules

---

### **3. Automatiser et coder l’infrastructure** <!--fit-->

---

Nous allons progressivement apprendre que manipuler Ansible consiste à écrire du texte géré sous forme de code informatique. L’ambition est donc de “coder l’infrastructure”. Alors comment coder l’infrastructure ? D’un point de vue historique, pour un parc de machines Linux, on commencera avec du Bash, ensuite probablement du Perl, et sans doute du Python. Or le personnel d’infrastructure s’il a choisi cette voie dans les métiers de l’informatique dipose de peu d’appétence pour une pratique de “développeur” d’autant plus que l’apprentissage d’un langage de programmation classique exigera une longue courbe d’apprentissage pour cetains profils.

---

Or Ansible permettra au personnel informatique d’automatiser les infrastructures. Il a l’avantage d’être :

- Populaire, diposant d’une communauté large,
- Flexible, sans limite sur les fonctions ou les cibles à gérer,
- Evolutif, aisé à adapter (en Python ou autres),
- Lisible par tous et à courbe d’apprentissage faible, grâce au format YAML.

Le seul écueil est de connaître les solutions à gérer à travers cet outil de telle sorte qu’une maîtrise d’une solution Ansible passe aussi par une bonne maîtrise de ce qui est déployé par Ansible.

Il faut alors voir Ansible comme une surcouche sans état (mis en intermédiaire qui fonctionne de manière très simple) qui intègre d’autres solutions ou s’intègre à d’autres facilement. Ansible Tower et son fork OpenSource AWX renforcent cette capacité de manière crédible en ajoutant des fonctions de gestion des utilisateurs, du code et des secrets.

---

### **4. Composants d'Ansible** <!--fit-->

---

![bg w:900](https://d33wubrfki0l68.cloudfront.net/a164b363e34dda928909d730081a7dc574f07155/90a4d/assets/images/ansible/linklight/how-ansible-works-diagram-01.svg.png)

---

En vue de contrôler des noeuds distants, des utilisateurs lancent des “playbooks” (livres de jeu) à partir d’un noeud de contrôle grâce à Ansible Engine.

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