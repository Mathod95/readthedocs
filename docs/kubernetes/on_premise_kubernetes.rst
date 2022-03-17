•	Installation de Kubernetes en interne
o	1. Objectifs du chapitre et prérequis
o	2. Installation à l’aide de Kubespray
	2.1 Origine du besoin
	2.2 Pourquoi Kubespray ?
	2.3 Principe de Kubespray
	2.4 Prérequis des machines à administrer avec Ansible
	2.4.1 Échange de clés SSH
	2.4.2 Escalade de droits sudo
	2.5 Structure du cluster
	2.5.1 Architecture du cluster Kubespray
	2.5.2 Groupes de machines
	2.6 Préparation des éléments d’installation
	2.6.1 Clonage du dépôt Git
	2.6.2 Installation des prérequis
	2.7 Préparation de l’inventaire Ansible
	2.7.1 Qu’est-ce qu’un inventaire ?
	2.7.2 Fichier d’inventaire d’exemple
	2.7.3 Test de la communication Ansible/SSH
	2.8 Installation du cluster
	2.8.1 Configuration du cluster
	2.8.2 Lancement de l’installation
	2.8.3 Mise à jour du cluster
	2.9 Accès au cluster
	2.9.1 Configuration de l’accès au cluster
	2.9.2 Utilisation d’un répartiteur de charge
	2.9.3 Vérification de la communication avec le cluster
o	3. Environnement embarqué avec k3s
	3.1 Présentation et but du projet
	3.2 Installation de k3s
	3.3 Lancement de k3s
	3.4 Communication avec le cluster
