•	Surveillance à l’aide de Prometheus
o	1. Objectifs du chapitre et prérequis
o	2. Mise en place de Prometheus
	2.1 À propos de Prometheus
	2.2 Fonctionnement de Prometheus
	2.2.1 Architecture de Prometheus
	2.2.2 Le moteur Prometheus
	2.2.3 Les exporteurs Prometheus
	2.3 Installation de Prometheus
	2.3.1 Choix du chart Prometheus
	2.3.2 Qu’est-ce qu’un opérateur ?
	2.3.3 Déploiement de l’opérateur Prometheus
	2.3.4 Pods démarrés
	2.3.5 Objets déploiements
	2.3.6 Nouvelles ressources Prometheus
	2.3.7 DaemonSet : node exporter
	2.4 Priorisation des briques de surveillance
	2.4.1 Problème de la surveillance
	2.4.2 Déclaration des classes de priorité
	2.4.3 Modification du déploiement de Prometheus
o	3. Utilisation de Prometheus
	3.1 Fonctionnement des métriques
	3.1.1 Consultation des métriques de Prometheus
	3.1.2 Présentation de l’interface de Prometheus
	3.1.3 Métriques de Kubernetes
	3.1.4 Déclaration des points de collecte dans Kubernetes
	3.1.5 Consultation des points de collecte dans Prometheus
	3.2 Définition des alertes
	3.2.1 Consultation de la liste des alertes
	3.2.2 Structure d’une règle d’alerte
	3.2.3 Définition d’alertes
	3.3 Gestionnaire d’alertes
	3.3.1 Rôle du gestionnaire d’alertes
	3.3.2 Consultation du gestionnaire d’alertes
	3.3.3 Configuration des alertes
	3.3.4 Désactivation des alertes scheduler et manager (clusters managés)
	3.3.5 Configuration de l'envoi des notifications
	3.3.6 Adresse de l’API de Slack
o	4. Tableaux de bord Grafana
	4.1 Présentation de Grafana
	4.2 Configuration de Grafana
	4.2.1 Branchement au moteur Prometheus
	4.2.2 Définition des tableaux de bord
	4.3 Interface Grafana
	4.4 Sécurisation de l'accès à Grafana
o	5. Suppression du chart de Prometheus

