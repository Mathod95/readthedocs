Maillage de services avec Istio
+++++++++++++++++++++++++++++++

Objectifs du chapitre et prérequis
==================================

Présentation d'Istio
====================

Micro-services et mise en réseau de services
--------------------------------------------

Présentation d’Istio
--------------------

Principe de fonctionnement
--------------------------

Installation d’Istio
====================

Configuration d'external-dns
----------------------------

Dépôt des charts Istio
----------------------

Installation du chart istio-init
--------------------------------

Installation du chart Istio
---------------------------

Activation des tableaux de bord
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Activation du mécanisme SDS
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configuration d'Istio
~~~~~~~~~~~~~~~~~~~~~

Installation d’Istio
~~~~~~~~~~~~~~~~~~~~

Configuration du gateway Istio
------------------------------

Présentation du mécanisme
~~~~~~~~~~~~~~~~~~~~~~~~~
Configuration du gateway
~~~~~~~~~~~~~~~~~~~~~~~~
Génération du certificat
~~~~~~~~~~~~~~~~~~~~~~~~

Utilisation d’Istio
===================
Injection de pods dans le maillage de services
----------------------------------------------

Installation d’istioctl
~~~~~~~~~~~~~~~~~~~~~~~
Injection du sidecar à l’aide d’istioctl
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Injection du sidecar par annotation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Désactivation du sidecar par annotation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Déploiement d’une application de test
-------------------------------------
Principe de l’exposition d’application avec Istio
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Préparation du fichier de déploiement MailHog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Déclaration du service MailHog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Création du gateway
~~~~~~~~~~~~~~~~~~~
Création du service virtuel (VirtualService)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sécurisation des flux
---------------------
Activation de Mutual TLS (mTLS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Consultation des polices du service MailHog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Forcer l’utilisation de mTLS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tableaux de bord
================
Présentation des différentes briques
------------------------------------
Interface Kiali
---------------
Interface Grafana
-----------------
Interface Jaeger
----------------