•	Compilation et stockage d’image Docker
o	1. Objectifs du chapitre et prérequis
o	2. Création d’une image Docker
	2.1 Application d’exemple Flask Healthcheck
	2.1.1 Présentation de l’application
	2.1.2 Présentation des dépendances
	2.1.3 Description des dépendances
	2.1.4 Installation des dépendances
	2.1.5 Initialisation de l’application
	2.1.6 Fonction racine
	2.1.7 Lancement du programme
	2.2 Environnement de compilation
	2.3 Le fichier Dockerfile
	2.3.1 Présentation du format
	2.3.2 Création de l’image
	2.3.3 Compilation et tag de l’image
	2.3.4 Authentification sur le registre d’images Docker
	2.3.5 Pousser l’image sur le registre
o	3. Image Docker multi-étape (multi-stage)
	3.1 Origine du besoin
	3.2 Exemple de compilation avec Maven
o	4. Analyse d’images
	4.1 Historique des commandes
	4.2 Analyse de l’image : Dive
	4.2.1 Présentation de Dive
	4.2.2 Installation de Dive
	4.2.3 Consultation du contenu d’une image
o	5. Utilisation de registres Docker privés
	5.1 Origine du besoin
	5.2 Déploiement d’image d’un registre privé
	5.2.1 Exposition de la problématique
	5.2.2 Création du secret
	5.2.3 Utilisation du secret
	5.2.4 Recopie d’un secret entre espaces de noms
	5.3 Erreurs de récupération des images
	5.3.1 Détection des erreurs
	5.3.2 Erreur sur le nom de l’image
	5.3.3 Secret absent ou non spécifié
	5.3.4 Identifiants invalides
	5.4 Services de registres managés
	5.4.1 Solutions managées
	5.4.2 Service Google Container Registry
	5.4.3 GitLab.com
