•	Usine logicielle
o	1. Objectifs du chapitre et prérequis
o	2. Compilation à l’aide de GitLab
	2.1 Application à compiler
	2.2 Mécanisme de pipeline GitLab
	2.3 Adresse et contenu du dépôt
	2.4 Structure du fichier .gitlab-ci.yml
	2.5 Exemple de fichier .gitlab-ci.yml de compilation d’image
	2.6 Pour la suite
o	3. Déploiement continu avec Jenkins
	3.1 À propos de Jenkins
	3.2 Installation de Jenkins
	3.2.1 Configuration du chart
	3.2.2 Vérification de l’installation
	3.2.3 Connexion à l’interface de Jenkins
	3.2.4 Installation d’extensions
o	4. Pipeline de déploiement continu avec Jenkins
	4.1 Prérequis
	4.2 Présentation du mécanisme de déploiement continu
	4.3 Stockage des identifiants Docker
	4.4 Création de l’environnement develop
	4.5 Création du pipeline
	4.5.1 Création du pod de compilation
	4.5.2 Squelette du pipeline de déploiement
	4.5.3 Récupération du code source
	4.5.4 Vérifications et tests
	4.5.5 Compilation de l’image Docker
	4.5.6 Connexion au registre et publication
	4.5.7 Mise à jour du déploiement de test
	4.5.8 Programme complet
	4.6 Lancement de la compilation
	4.6.1 Création du job
	4.6.2 Lancement du build
	4.7 Compte de service
	4.7.1 Opérations à réaliser
	4.7.2 Création d’un compte de service
	4.7.3 Création du rôle de mise à jour
	4.7.4 Affectation du rôle au compte de service
	4.7.5 Affectation du compte de service
	4.7.6 Relance de la compilation
	4.8 Mécanisme de Webhook
	4.8.1 Présentation du mécanisme
	4.8.2 Déclenchement du Webhook
	4.8.3 Création du Webhook
o	5. Un mot sur Jenkins X
