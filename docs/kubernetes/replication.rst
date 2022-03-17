•	Mise en place d’une réplication entre pods
o	1. Objectifs du chapitre et prérequis
o	2. Synchronisation des pods MariaDB
	2.1 Exposition de la problématique
	2.2 Principe de fonctionnement de la synchronisation
	2.2.1 Opérations à réaliser
	2.2.2 Nombre de réplicats
	2.3 Identifiants des serveurs
	2.3.1 Connexion aux pods
	2.3.2 Connexion à la base de données
	2.3.3 Identifiants des serveurs
	2.3.4 ID du maître
	2.3.5 Création du compte de réplication sur le maître
	2.3.6 Configuration de l’esclave
	2.4 Activation de la synchronisation
	2.4.1 Activer les journaux pour la réplication
	2.4.2 Commande docker-entrypoint.sh
	2.4.3 Consultation de l’état du maître
	2.4.4 Configuration de l’esclave
	2.5 Test de la réplication
	2.5.1 Connexion au maître
	2.5.2 Création d’une table
	2.5.3 Connexion à l’esclave
o	3. Automatisation de la synchronisation
	3.1 Scripts de démarrage et synchronisation
	3.1.1 Script de démarrage
	3.1.2 Configuration de la synchronisation
	3.1.3 Scripts SQL additionnels
	3.1.4 Script d’arrêt de la base
	3.2 Scripts et objet ConfigMap
	3.3 Création du ConfigMap
	3.4 Montage du ConfigMap
	3.4.1 Référencement du ConfigMap dans la liste des volumes
	3.4.2 Point de montage du ConfigMap
	3.5 Démarrage et arrêt du container
	3.5.1 Commande de démarrage
	3.5.2 Commande d’arrêt de la base
	3.6 Résumé des modifications
	3.7 État du déploiement
	3.7.1 État des pods
	3.7.2 Journaux d’activité du pod esclave
	3.7.3 Test de la synchronisation
	3.7.4 Vérification du fonctionnement de la synchronisation
