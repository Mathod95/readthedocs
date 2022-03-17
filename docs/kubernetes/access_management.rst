•	Restriction et délégation d’accès
o	1. Objectifs du chapitre et prérequis
o	2. Mise en place de quotas
	2.1 Origine du besoin
	2.2 Quotas par défaut sur un espace de noms
	2.2.1 Création d’un espace de noms
	2.2.2 Structure d’un objet LimitRange
	2.2.3 Exemple de définition de limitations
	2.2.4 Vérification de l’application des limitations
	2.2.5 Test du mécanisme
	2.2.6 Analyse du problème
	2.3 Quotas globaux sur un espace de noms
	2.3.1 Présentation des quotas de ressources (ResourceQuota)
	2.3.2 Structure d’un quota de ressources
	2.3.3 Exemples de restriction de consommation CPU et mémoire
	2.3.4 Champs pour positionner des limitations (champ hard)
	2.3.5 Test du mécanisme
	2.3.6 Nettoyage en fin d’exercice
o	3. Authentification et autorisation
	3.1 Origine du besoin
	3.2 Prérequis
	3.3 Activation des accès anonymes
	3.3.1 Activation des accès anonymes sur Minikube
	3.3.2 Création du fichier d’accès
	3.3.3 Affectation des droits en lecture
	3.3.4 Suppression des droits d’accès anonymes
	3.4 Principe de l’authentification par certificat
	3.5 Problème de la révocation des certificats
	3.6 Génération du certificat
	3.6.1 Création de la clé et du certificat client
	3.6.2 Emplacement de la PKI
	3.6.3 Signature du certificat
	3.7 Authentification par certificat
	3.7.1 Récupération des informations de connexion au cluster
	3.7.2 Utilisation du certificat pour l’authentification
	3.7.3 Test de la connexion
	3.8 Quelques exemples d’erreurs de manipulation
	3.8.1 Problème d’autorité de certification
	3.8.2 Problème de couple clé/certificat
	3.8.3 Pas d’identifiant renseigné
	3.8.4 Utilisation de la demande de certificat à la place du certificat
	3.9 Attributions de droits administrateur sur le cluster
	3.9.1 Contexte et opérations à réaliser
	3.9.2 Affectation des droits administrateur à un utilisateur
	3.9.3 Test du nouvel administrateur
	3.9.4 Création de nouveaux utilisateurs
	3.9.5 Affectation des droits administrateur à un groupe
	3.9.6 Administrateur d’un espace de noms
o	4. Mécanismes d’authentification externes
	4.1 Présentation du mécanisme
	4.2 Communication entre le fournisseur OAuth2 et le cluster
	4.3 Création des identifiants
	4.4 Modification des options de démarrage (Minikube)
	4.5 Configuration des accès clients
	4.5.1 Présentation de l’outil k8s-oidc-helper
	4.5.2 Installation du compilateur Go
	4.5.3 Installation de k8s-oidc-helper
	4.5.4 Génération des identifiants d’accès
	4.5.5 Renseignement du cluster et contexte
	4.5.6 Test de connexion
	4.6 Attribution des droits d’accès
