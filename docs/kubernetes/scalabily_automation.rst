•	Montée en charge automatique
o	1. Objectifs du chapitre et prérequis
o	2. Le serveur de métriques
	2.1 Présentation de la brique metrics-server
	2.2 Activation du serveur de métriques
	2.2.1 Vérification de la présence du serveur de métriques
	2.2.2 Activation sous Minikube
	2.2.3 Activation sur Amazon EKS
	2.3 Consultation de la consommation des pods et des nœuds
	2.3.1 État des nœuds d’un cluster
	2.3.2 État des pods
o	3. Activation de la montée en charge automatique
	3.1 Test avec l’application MailHog
	3.2 Lancement d’un bench
	3.2.1 Présentation d’Apache Bench
	3.2.2 Installation d'Apache Bench
	3.2.3 Lancement du test initial
	3.3 Gestion de la montée en charge
	3.4 Lancement du test
	3.4.1 Test à froid : montée en charge des pods
	3.4.2 Test à chaud
	3.4.3 Diminution du nombre de pods
o	4. Scalabilité des nœuds d’un cluster
	4.1 Contexte
	4.2 Présentation de l’autoscaler
	4.3 Activation de l’autoscaler avec Google Cloud
	4.4 Activation de l'autoscaler avec Azure AKS
	4.5 Activation de l'autoscaler avec Amazon EKS
	4.5.1 Présentation du mécanisme de l’ASG
	4.5.2 Affichage des tags d’un groupe ASG
	4.5.3 Activation de l’autoscaler
	4.5.4 Vérification de l'activation du mécanisme de l’autoscaler
	4.6 Test de montée en charge
	4.6.1 Déploiement de WordPress
	4.6.2 Pods en attente de ressources
	4.6.3 État des nœuds
	4.6.4 Démarrage du pod
	4.6.5 Nettoyage des déploiements
