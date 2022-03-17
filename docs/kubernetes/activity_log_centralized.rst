•	Centralisation des journaux d’activité
o	1. Objectifs du chapitre et prérequis
o	2. Principe de la centralisation des journaux
	2.1 Architecture
	2.2 Caractéristiques de l’agent déployé
	2.3 Mécanisme de centralisation des journaux
o	3. Centralisation dans le cloud
	3.1 Centralisation à l’aide d’un service managé
	3.2 Google Stackdriver
	3.2.1 Présentation de Stackdriver
	3.2.2 Pod Fluentd (cluster GKE)
	3.2.3 Consultation des journaux
	3.3 Azure Monitor
	3.3.1 Présentation d'Azure Monitor
	3.3.2 Consultation des journaux
	3.4 Amazon Cloudwatch
	3.4.1 Présentation de Cloudwatch
	3.4.2 Activation de Cloudwatch sur le centre de contrôle
	3.4.3 Configuration de Cloudwatch
	3.4.4 Création de la police de communication avec Cloudwatch
	3.4.5 Création d’un compte et rattachement à la police
	3.4.6 Création d’une clé d’accès
	3.4.7 Envoi des journaux dans Cloudwatch
	3.4.8 État des pods déployés
	3.4.9 Consultation des journaux dans Cloudwatch
o	4. Centralisation des journaux avec Loki
	4.1 Présentation de Loki
	4.1.1 Origine de Loki
	4.1.2 Loki vs Elasticsearch
	4.1.3 Conseil d’utilisation
	4.2 Installation de Loki
	4.3 Configuration de la source de données Grafana
	4.4 Consultation des journaux dans Grafana
	4.4.1 Vérification des sources de données
	4.4.2 Consultation des journaux
o	5. Centralisation des journaux avec Elasticsearch
	5.1 Avertissements et limitations
	5.2 À propos d’Elasticsearch
	5.3 Déploiement des briques Elasticsearch
	5.3.1 Installation d’Elasticsearch
	5.3.2 Installation de l’agent fluent-bit
	5.3.3 Installation de Kibana
	5.3.4 Installation de Cerebro
	5.4 État des différentes briques
	5.4.1 État du moteur Elasticsearch
	5.4.2 Agent fluent-bit
o	6. Gestion d’Elasticsearch
	6.1 Accès à l’interface Cerebro
	6.2 Utilisation de Kibana
	6.2.1 Accéder à l’interface de Kibana
	6.2.2 Création de l’index
	6.3 Branchement sur Grafana
	6.3.1 Source de données Elasticsearch
	6.3.2 Création d’un objet ConfigMap
