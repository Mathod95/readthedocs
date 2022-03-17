•	Hébergement d’application en cluster
o	1. Objectifs du chapitre et prérequis
o	2. Déploiement d’une base de données MariaDB
	2.1 Origine du besoin
	2.2 Déploiement
	2.2.1 Choix de l’image Docker
	2.2.2 Version initiale du fichier de déploiement
	2.2.3 Gestion de la réentrance
	2.3 Volume persistant
	2.3.1 Demande de volume persistant
	2.3.2 État de la demande de volume persistant
	2.3.3 Ajout d’une persistance sur le container de MariaDB
	2.3.4 Consultation de l'état du déploiement
	2.4 Configuration de la base de données
	2.5 Consultation de l’état du pod
	2.5.1 Liste des pods
	2.5.2 Connexion au container
	2.6 Surveillance de la base de données
	2.6.1 Définition des commandes de surveillance
	2.6.2 Application de la modification
	2.6.3 Vérification du déploiement
	2.7 Mécanisme de déploiement
o	3. Mise en place d’un StatefulSet
	3.1 Augmentation du nombre de pods associés au déploiement
	3.2 Présentation du type StatefulSet
	3.2.1 Caractéristiques
	3.2.2 Limitations
	3.3 Déclaration du premier objet StatefulSet
	3.3.1 Purge de l’ancien déploiement
	3.3.2 Modifications à réaliser
	3.3.3 Création du StatefulSet
	3.3.4 État des volumes persistants
	3.3.5 Suppression des anciens objets PV/PVC
	3.4 Scalabilité de l’objet StatefulSet
	3.5 Pods et volumes persistants d’un objet StatefulSet
	3.6 Réduction de la taille du StatefulSet
o	4. Base et compte de test
	4.1 Variables d’environnement du container
	4.2 ConfigMap et secret
	4.2.1 Pourquoi y faire appel ?
	4.2.2 Structure d’un objet ConfigMap
	4.2.3 Déclaration d’un objet Secret
	4.2.4 Rattachement au container
