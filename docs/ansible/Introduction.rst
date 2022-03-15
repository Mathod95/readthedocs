Introduction
++++++++++++

.. image:: https://raw.githubusercontent.com/Mathod95/ANSIBLE/master/docs/Ansible/img/ansible_logo.png
  :alt: Ansible_Logo
  :scale: 100
  :align: center

`Ansible <https://www.redhat.com/fr/technologies/management/ansible>`_ outil incontournable de gestion d’infrastructure ayant pour target principale les systemes Linux. Il est capable de représenter la gestion de la configuration d’une infrastructure sous forme de code aisé à lire et à gérer. 

En guise d’introduction, on décrira dans ce document le projet Ansible, ses cas d’usage, ses composants, son principe de fonctionnement, son installation et les différents binaires qui l’accompagnent.

Après des généralités, le document décrit la terminologie et les composants Ansible. Il indique les procédures d’installation de Ansible sur une machine ControlNode Debian.

On tentera ici de comprendre de manière sommaire les composants de base d’Ansible tels que les connexions selon les cibles, les inventaires, les modules, les collections, le mode ad-hoc, les variables, les “Facts”, les playbooks, les fichiers de configuration YAML, les sorties JSON et les modèles Jinja2, les rôles, Ansible AWX, l’idempotence.

Enfin, on ne manquera de décrire l’environnement d’exécution d’Ansible en décrivant les différentes commandes ansible disponibles nativement.

Prerequisites
=============

Pour aborder ce document quelques pré-requis sont nécessaires :

* Avoir les notions de base en administration Linux de base (Utilisateurs, fichiers, services, réseau, stockage, système de fichiers, pare-feu, Selinux, etc.)
* Maîtriser un éditeur de texte comme vim
* Maîtriser un SCM comme git
* Avoir des notions de virtualisation logicielle et/ou matérielle

Objectif atteints grace à Ansible:

* Le minimum par nature. Les systèmes de gestion ne devraient pas imposer des dépendances supplémentaires sur l’environnement.
* La cohérence. cf. notion de test unitaire (procédure permettant de vérifier le bon fonctionnement d’une partie précise d’un logiciel ou d’une portion d’un programme).
* La sécurité. Ansible ne déploie pas des agents sur les noeuds. Un protocole de transport comme OpenSSH ou HTTPS est seulement nécessaire pour commencer une gestion.
* La fiabilité. Lorsqu’il est écrit soigneusement, un livre de jeu Ansible peut être idempotent afin d’éviter des effets secondaires inattendus sur les systèmes gérés.
* Une courbe d’apprentissage faible. Les livres de jeux Ansible utilisent un langage simple et descriptif basé sur YAML et les modèles Jinja2.




