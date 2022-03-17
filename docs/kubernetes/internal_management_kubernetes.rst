•	Gestion des briques internes de Kubernetes
o	1. Objectifs du chapitre et prérequis
o	2. Espace de noms kube-system
	2.1 Pods présents dans l’espace de noms kube-system
	2.2 CoreDNS
	2.3 etcd
	2.4 Le gestionnaire d’extensions de Minikube
	2.5 Le serveur d'API
	2.6 Le proxy Kubernetes (kube-proxy)
	2.7 Le gestionnaire de tâches (scheduler)
	2.8 Le gestionnaire de contrôle (controller manager)
	2.9 Kubelet
o	3. Configuration des serveurs maîtres
	3.1 Principe de lancement des pods système
	3.2 Contenu du répertoire /etc/kubernetes/manifests
	3.3 Contenu des fichiers
	3.4 Désactivation d’un pod système
	3.5 Réactivation du pod système
o	4. Monitoring des containers du cluster avec Glances
	4.1 Origine du besoin
	4.2 Consultation des DaemonSets
	4.3 Présentation de Glances
	4.4 Définition du DaemonSet
	4.4.1 Structure de la déclaration
	4.4.2 Champ volumes
	4.4.3 Champ containers
	4.5 Création du DaemonSet
	4.5.1 Déclaration complète
	4.5.2 Création du DaemonSet
	4.5.3 Consultation des pods
	4.6 Annotations de tolérance
	4.6.1 Présentation du mécanisme
	4.6.2 Récupération des annotations taints
	4.6.3 Tolérances de lancement
	4.6.4 Modification du DaemonSet
	4.7 Connexion à Glances
