•	Helm - Gestionnaire de package
o	1. Objectifs du chapitre et prérequis
o	2. Présentation de Helm
	2.1 Pourquoi faire appel à Helm ?
	2.2 Principe de fonctionnement
o	3. Déploiement de Helm
	3.1 Installation du client Helm
	3.2 Consultation de la version de Helm
	3.3 Configuration du client Helm
	3.4 Initialisation de la partie serveur (Tiller) avec Helm 2.x
	3.4.1 Un mot sur la sécurité (Helm 2.x)
	3.4.2 Le compte de service de Tiller (Helm 2.x)
	3.4.3 Création du compte de service
	3.4.4 Attribution des droits d’administrateur au compte de service
	3.4.5 Initialisation de Tiller
	3.5 Suppression de Tiller (Helm 2)
o	4. Déploiement d’une application avec Helm
	4.1 Déterminer le package à déployer
	4.2 Installation du package Wordpress
	4.2.1 Un peu de vocabulaire
	4.2.2 Installation avec Tiller
	4.2.3 Installation sans Tiller
	4.3 Corrections de l’installation
	4.3.1 Quelques remarques
	4.3.2 Spécification du nom et espace de noms
	4.3.3 Lancement de l’installation
	4.3.4 Mise à jour et réentrance
	4.4 Éléments déployés avec Helm
	4.5 Suppression d’un déploiement
	4.6 Annulation de la suppression
	4.7 Purge d’un chart Helm
o	5. Cycle de vie d’une application déployée avec Helm
	5.1 Ouverture du port vers WordPress
	5.2 Connexion à WordPress
	5.3 Configuration d’un chart Helm
	5.3.1 Consultation des options d’un chart
	5.3.2 Configuration de la publication (Minikube)
	5.4 Historique de déploiement
	5.5 Retour arrière
	5.6 Portail Helm Hub
