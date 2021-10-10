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