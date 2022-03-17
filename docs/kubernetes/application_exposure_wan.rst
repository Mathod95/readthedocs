•	Exposition des applications sur Internet
o	1. Objectifs du chapitre et prérequis
o	2. Gestion des entrées DNS
	2.1 Principe de fonctionnement
	2.2 Prérequis
	2.3 Retour sur le fonctionnement du domaine DNS nip.io
	2.4 Activation du service DNS
	2.4.1 Console Cloud DNS Google
	2.4.2 Service DNS Zones d’Azure
	2.4.3 Service Route 53 d’AWS
	2.5 Configuration DNS
	2.5.1 Opération à réaliser
	2.5.2 Console DNS OVH
	2.5.3 Vérification de la délégation
	2.6 Gestionnaire de DNS
	2.6.1 Présentation de la brique external-dns
	2.6.2 Création du compte d’administration DNS de Google Cloud
	2.6.3 Création du compte d’administration DNS service Azure
	2.6.4 Création du compte d’administration DNS Amazon (Route 53)
	2.6.5 Création d’un secret (Google et Azure)
	2.6.6 Déploiement d’external-dns
	2.6.7 Vérification du fonctionnement d’external-dns
o	3. Exposition de services et répartition de charge
	3.1 Présentation du mécanisme
	3.2 Retour sur la notion de service
	3.2.1 Rôle d’un service
	3.2.2 Structure d’un service
	3.2.3 Type ClusterIP
	3.2.4 Type NodePort et LoadBalancer
	3.2.5 Type ExternalName
	3.3 Service associé au proxy inverse
o	4. Le contrôleur Ingress
	4.1 Principe de fonctionnement
	4.2 Le rôle du contrôleur Ingress
	4.3 Structure d’une règle Ingress
	4.4 Droits nécessaires pour un contrôleur
o	5. Le contrôleur Ingress Google
	5.1 Prérequis
	5.2 Présentation du contrôleur GLBC
	5.3 Déploiement de MailHog
	5.3.1 Préparation de la règle Ingress
	5.3.2 Déploiement de l’application MailHog
	5.3.3 Consultation de l’état de l’objet Ingress
	5.3.4 Consultation du journal d'activité d’external-dns
	5.3.5 Consultation de MailHog
o	6. Le contrôleur Ingress Nginx
	6.1 Pourquoi changer de contrôleur Ingress ?
	6.2 Présentation du logiciel Nginx
	6.3 Installation d’Ingress Nginx sur GKE (Google)
	6.3.1 Détermination du chart Helm à installer
	6.3.2 Espace de noms et configuration du chart
	6.4 Utilisation du contrôleur
	6.4.1 Utilisation de l’annotation kubernetes.io/ingress.class
	6.4.2 Vérification du déploiement
	6.5 Annotations Ingress Nginx
o	7. Le contrôleur Ingress Traefik
	7.1 Présentation de Traefik
	7.2 Installation du chart Helm
	7.3 Utilisation du nouveau contrôleur Ingress
	7.3.1 Sélectionner le contrôleur Ingress Traefik
	7.3.2 Création de la règle Ingress faisant appel à Traefik
	7.3.3 État des règles Ingress
	7.4 Tableau de bord de Traefik
	7.5 Annotations Ingress Traefik
