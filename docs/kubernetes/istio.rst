•	Maillage de services avec Istio
o	1. Objectifs du chapitre et prérequis
o	2. Présentation d'Istio
	2.1 Micro-services et mise en réseau de services
	2.2 Présentation d’Istio
	2.3 Principe de fonctionnement
o	3. Installation d’Istio
	3.1 Configuration d'external-dns
	3.2 Dépôt des charts Istio
	3.3 Installation du chart istio-init
	3.4 Installation du chart Istio
	3.4.1 Activation des tableaux de bord
	3.4.2 Activation du mécanisme SDS
	3.4.3 Configuration d'Istio
	3.4.4 Installation d’Istio
	3.5 Configuration du gateway Istio
	3.5.1 Présentation du mécanisme
	3.5.2 Configuration du gateway
	3.5.3 Génération du certificat
o	4. Utilisation d’Istio
	4.1 Injection de pods dans le maillage de services
	4.1.1 Installation d’istioctl
	4.1.2 Injection du sidecar à l’aide d’istioctl
	4.1.3 Injection du sidecar par annotation
	4.1.4 Désactivation du sidecar par annotation
	4.2 Déploiement d’une application de test
	4.2.1 Principe de l’exposition d’application avec Istio
	4.2.2 Préparation du fichier de déploiement MailHog
	4.2.3 Déclaration du service MailHog
	4.2.4 Création du gateway
	4.2.5 Création du service virtuel (VirtualService)
	4.3 Sécurisation des flux
	4.3.1 Activation de Mutual TLS (mTLS)
	4.3.2 Consultation des polices du service MailHog
	4.3.3 Forcer l’utilisation de mTLS
o	5. Tableaux de bord
	5.1 Présentation des différentes briques
	5.2 Interface Kiali
	5.3 Interface Grafana
	5.4 Interface Jaeger
