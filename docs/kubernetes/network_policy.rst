•	Polices réseau
o	1. Objectifs du chapitre et prérequis
o	2. Les polices réseau (network policies)
	2.1 Présentation du mécanisme
	2.2 Kubernetes Network Plugins
	2.3 Polices réseau sur services managés et installation maison
	2.4 Installation de Calico sur Minikube
	2.4.1 Activation de CNI sur Minikube
	2.4.2 Installation de Calico
	2.5 Connexions entrantes
	2.5.1 Test de la connexion en interne
	2.5.2 Bloquer les accès internes
	2.5.3 Test de la règle
	2.6 Connexions sortantes
	2.6.1 Test des connexions externes
	2.6.2 Restriction sur les règles sortantes
	2.6.3 Test de la règle
o	3. Protection de l’application WordPress
	3.1 Contexte
	3.2 Déploiement de WordPress
	3.3 Restriction des accès
	3.3.1 Référencement de l’ensemble des flux
	3.3.2 Restriction de tous les accès
	3.3.3 Autorisation de l'accès du contrôleur Ingress sur WordPress
	3.3.4 Autorisation de l'accès entre WordPress et MariaDB
	3.3.5 Test des règles réseau
	3.4 Ressources externes
