•	Persistance des données
o	1. Objectifs du chapitre et prérequis
o	2. Persistance des données
	2.1 Origine du besoin
	2.2 Utilisation d’un volume persistant externe
	2.3 Volumes persistants
	2.3.1 Structure du volume persistant
	2.3.2 Création du volume persistant
	2.4 Persistance de données avec MailHog
	2.4.1 Opérations à réaliser
	2.4.2 Déclaration de l’objet PersistentVolumeClaim
	2.4.3 État des objets de volume persistant
	2.4.4 État de la demande de volume persistant
	2.4.5 Déclaration du point de montage
	2.4.6 Ajout d’un point de montage sur le container
	2.4.7 Options de lancement de MailHog
	2.4.8 Déclaration entière suite aux modifications
	2.5 Test de la persistance
	2.5.1 Installation de mhsendmail
	2.5.2 Ouverture de la communication avec le port SMTP
	2.5.3 Envoi d’un mail
	2.5.4 Droits du répertoire de persistance des données
	2.5.5 Consultation de l’interface MailHog
	2.5.6 Suppression des pods
	2.5.7 Vérification du fonctionnement de la persistance
o	3. Classes de stockage
	3.1 Origine du besoin
	3.2 Liste des classes de stockage
	3.3 Détail d’une classe de stockage
	3.4 Classe de stockage par défaut
	3.5 Les différentes classes de stockage
	3.5.1 Les différentes familles
	3.5.2 Origine de ces familles
	3.6 Caractéristiques des classes de stockage
	3.6.1 Modes d’accès
	3.6.2 Caractéristiques de certains pilotes
	3.6.3 Liste des pilotes chargés
	3.7 Déclaration d’une classe de stockage
	3.7.1 Structure de la déclaration
	3.7.2 Exemple de déclaration
	3.8 Test de création automatique d’un volume persistant
