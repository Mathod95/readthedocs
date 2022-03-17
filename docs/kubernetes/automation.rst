Automatisation et publication d’une application
+++++++++++++++++++++++++++++++++++++++++++++++
Objectifs du chapitre et prérequis
==================================
Gestion par kubectl d’une application
=====================================
Suppression d’un déploiement
----------------------------
Création d’un déploiement
-------------------------
État du déploiement
-------------------
Mécanisme des réplicats
-----------------------
Consultation des réplicats
~~~~~~~~~~~~~~~~~~~~~~~~~~
Description des réplicats
~~~~~~~~~~~~~~~~~~~~~~~~~
État du pod
-----------
Liste des pods
~~~~~~~~~~~~~~
Détails de l’état d’un pod
~~~~~~~~~~~~~~~~~~~~~~~~~~
Accès aux logs des containers
-----------------------------
Accéder à l’application MailHog
-------------------------------
Exposition de services
======================
Pourquoi utiliser un service ?
------------------------------
Exposition d’un déploiement via un service
------------------------------------------
Vérification du service mailhog
-------------------------------
Que faire en cas d’absence de shell ?
-------------------------------------
Résilience et scalabilité
-------------------------
Origine du besoin
~~~~~~~~~~~~~~~~~
Scalabilité manuelle
~~~~~~~~~~~~~~~~~~~~
Nombre de pods associés à un déploiement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Arrêter temporairement une application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Automatisation de déploiement par fichier YAML
==============================================
Mécanisme de création et mise à jour
------------------------------------
Structure YAML d’un déploiement
-------------------------------
Quelques rappels
~~~~~~~~~~~~~~~~
Récupération d’une structure au format YAML
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Édition d’un déploiement
~~~~~~~~~~~~~~~~~~~~~~~~
Squelette pour un déploiement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Création d’un déploiement à l’aide d’un fichier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Suppression des éléments d’un fichier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gestion de l’idempotence et de la réentrance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Création du service
-------------------
Définition du service
~~~~~~~~~~~~~~~~~~~~~
Application de la définition du service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gestion de la réentrance
~~~~~~~~~~~~~~~~~~~~~~~~
Mécanisme de sélecteur et labels
--------------------------------
Regroupement de la création des éléments
----------------------------------------
Création d’un groupe d’objets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Consultation de l’état d’un groupe d’objets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Structure des objets
--------------------
Interrogation de Kubernetes avec kubectl
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Référence de l’API en ligne
~~~~~~~~~~~~~~~~~~~~~~~~~~~
Ingress et reverse proxy
========================
Origine du besoin
-----------------
Activation du contrôleur Ingress dans Minikube
----------------------------------------------
Déclaration d’une règle Ingress
-------------------------------
Consultation des règles Ingress
-------------------------------
Désactivation de la redirection HTTP vers HTTPS
-----------------------------------------------
Hôte virtuel et nip.io
----------------------
Hôte virtuel par défaut
~~~~~~~~~~~~~~~~~~~~~~~
Présentation du mécanisme de nip.io
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Création d’un hôte virtuel pour mailhog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
