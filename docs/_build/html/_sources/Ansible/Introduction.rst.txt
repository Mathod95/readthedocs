Introduction
++++++++++++

.. image:: https://cdn.icon-icons.com/icons2/2699/PNG/512/ansible_logo_icon_169596.png
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

Présentation de Ansible
=======================

Ansible est un outil open-source de provisionnement de logiciels, de gestion des configurations et de déploiement d’applications qui permet de faire de l’IaC. Il fonctionne sur de nombreux systèmes de type Unix et peut configurer aussi bien des systèmes Microsoft Windows. Il comprend son propre langage **déclaratif** pour décrire la configuration du système. Ansible est agent-less, se connectant temporairement à distance via SSH ou Windows Remote Management (permettant l’exécution à distance de PowerShell) pour effectuer ses tâches.

Ansible gère les différents noeuds avec un accès à distance natif (tels que les protocoles SSH ou Remote PowerShell ou encore des APIs natives). Il ne nécessite l’installation d’aucun logiciel supplémentaire à distance. Il offre des capacités de parallélisation, collecte de métadonnées et gestion des états. Cet aspect de conception “sans agent” installé sur le périphérique est important car il réduit les besoins d’infrastructure pour démarrer une gestion. Les modules fonctionnent grâce à JSON et à la sortie standard et peuvent être écrits dans n’importe quel langage de programmation.Le système utilise notamment YAML pour exprimer des descriptions réutilisables de systèmes, il fournit des sorties en JSON, il traite les variables grâce à des modèles Jinja2.

Le logiciel Ansible a été conçu par un ancien employé Red Hat, Michael DeHaan, également auteur de l’application de serveur de “provisionning” Cobbler et co-auteur du framework Func pour l’administration à distance. Le code source du logiciel est sous licence GNU General Public v3.0. Red Hat a racheté la société Ansible, Inc. en octobre 2015[¹].


Installing Ansible
==================

Installing Ansible via PPA
--------------------------

Upgrade Ansible via PPA
~~~~~~~~~~~~~~~~~~~~~~~

Installing Ansible via PIP
--------------------------

Upgrade Ansible via PIP
~~~~~~~~~~~~~~~~~~~~~~~
