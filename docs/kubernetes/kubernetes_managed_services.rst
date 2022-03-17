•	Services managés Kubernetes
o	1. Objectifs du chapitre et prérequis
o	2. Service managé de Google : GKE
	2.1 Présentation du service Google
	2.2 Administration depuis la console Google
	2.3 Installation de la commande gcloud en local
	2.3.1 Installation sur Debian/Ubuntu
	2.3.2 Mise en place de l’autocomplétion
	2.4 Configuration de l'environnement
	2.4.1 Authentification auprès de Google Cloud
	2.4.2 Projet associé avec le contexte courant
	2.4.3 Activation de l’API
	2.5 Gestion du cluster GKE
	2.5.1 Consultation de la liste des clusters
	2.5.2 Versions et régions disponibles
	2.6 Création d’un cluster
	2.6.1 Options de création
	2.6.2 Lancement de la création du cluster
	2.6.3 Récupération du fichier d’accès au cluster
	2.7 Consultation du cluster
	2.7.1 Liste des nœuds
	2.7.2 Services démarrés
	2.8 Délégation des droits d’accès
	2.8.1 Configuration des accès
	2.8.2 Principe du mécanisme sous-jacent
	2.9 Configuration de Helm/Tiller 2.x
	2.10 Suppression d’un cluster GKE
o	3. Service managé Microsoft Azure : AKS
	3.1 Présentation du service Azure
	3.2 Administration depuis la console Azure
	3.2.1 Présentation de la console
	3.2.2 Consultation du tableau de bord Kubernetes
	3.3 Installation de la commande az en local
	3.3.1 Installation sur Debian/Ubuntu
	3.3.2 Mise en place de l'autocomplétion
	3.4 Authentification auprès du service Azure
	3.5 Emplacement de déploiement
	3.5.1 Liste des emplacements
	3.5.2 Versions disponibles de Kubernetes
	3.6 Création d’un cluster
	3.6.1 Création d’un groupe de ressources
	3.6.2 Lancement de la création du cluster
	3.6.3 Récupération du fichier de connexion
	3.6.4 Zone DNS par défaut
	3.7 Consultation de la liste des clusters
	3.8 Délégation des droits d’accès
	3.9 Configuration de Helm/Tiller 2.x
	3.10 Suppression d’un cluster AKS
o	4. Service managé d’Amazon : EKS
	4.1 Présentation du service Amazon AWS
	4.2 Introduction de la commande eksctl
	4.3 Configuration des accès Amazon
	4.4 Installation des binaires
	4.4.1 Installation d’eksctl à l’aide de snap
	4.4.2 Installation de l’outil aws cli
	4.4.3 Vérification de la communication avec AWS
	4.5 Création du cluster EKS
	4.5.1 Aide en ligne d’eksctl
	4.5.2 Options intéressantes à la création d’un cluster
	4.5.3 Lancement de la création du cluster
	4.6 Configuration des accès kubectl
	4.7 Installation de aws-iam-authenticator
	4.8 Délégation des droits d’accès
	4.8.1 Configuration des accès
	4.8.2 Principe du mécanisme sous-jacent
	4.9 Configuration de Helm/Tiller 2.x
	4.10 Suppression du cluster
o	5. Accès en lecture-écriture multiple
	5.1 Origine du besoin
	5.2 Serveur NFS déployé dans Kubernetes
	5.2.1 Limitations
	5.2.2 Déploiement d’un serveur NFS
	5.2.3 Vérification du déploiement
	5.2.4 Test de création de volume persistant (PVC)
	5.3 Service managé Amazon : EFS
	5.3.1 Consultation des instances EFS
	5.3.2 Création d’une instance EFS
	5.3.3 Déploiement de la classe de stockage EFS
	5.4 Service managé Google : Filestore
	5.4.1 Consultation des instances Filestore
	5.4.2 Création d’une instance Filestore
	5.5 Classe de stockage NFS
	5.5.1 Installation du chart
	5.5.2 Vérification de l'installation du chart
	5.5.3 Test de création d’une demande de volume persistant (PVC)
	5.6 Classe de stockage Azure
