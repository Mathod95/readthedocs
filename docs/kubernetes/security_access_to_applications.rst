•	Sécurisation : accès aux applications
o	1. Objectifs du chapitre et prérequis
o	2. Mise en place de Let’s Encrypt
	2.1 Présentation de Let’s Encrypt
	2.2 Installation du chart Helm cert-manager
	2.2.1 Présentation du chart Helm
	2.2.2 Prérequis avant installation
	2.3 L’émetteur de certificats (issuer)
	2.3.1 Principe du protocole ACME
	2.3.2 Structure de la déclaration d’un émetteur
	2.3.3 Exemple de déclaration Issuer Google
	2.3.4 Exemple de déclaration Issuer Azure
	2.3.5 Exemple de déclaration Issuer Amazon
	2.3.6 Limitations et certificats avec joker
	2.4 Exemples de déclarations
	2.4.1 Serveur Let’s Encrypt de test
	2.4.2 Serveur Let’s Encrypt de production
	2.5 Déclaration des certificats
	2.5.1 État des émetteurs de certificats
	2.5.2 Structure d’un certificat
	2.5.3 Certificat de test
	2.5.4 État du certificat
	2.5.5 Journal d’activité de cert-manager
	2.5.6 Consultation du secret
	2.5.7 Certificat de production
	2.5.8 Marche à suivre en cas de problèmes
	2.6 Rattachement du certificat à la règle Ingress
	2.7 Automatisation de la gestion des certificats
	2.7.1 Certificat par défaut du contrôleur Ingress Nginx
	2.7.2 Mécanisme d’annotations
	2.7.3 Émetteur de certificats par défaut
o	3. Protection de l’accès aux applications
	3.1 Origine du besoin
	3.2 Mot de passe simple (HTTP basic)
	3.2.1 Principe de fonctionnement
	3.2.2 Création du secret à l’aide de htpasswd
	3.2.3 Import du secret
	3.2.4 Configuration de l’authentification
o	4. Authentification basée sur OAuth2
	4.1 À propos du protocole OAuth2
	4.2 Principe de la solution
	4.3 Création d’un identifiant GitHub
	4.4 Déploiement du proxy
	4.4.1 À propos du proxy
	4.4.2 Configuration du chart Helm
	4.4.3 Déploiement du chart Helm
	4.4.4 État du déploiement
	4.5 Déclaration des règles Ingress
	4.5.1 Description des règles Ingress
	4.5.2 Annotations Ingress de MailHog
	4.5.3 Description Ingress du proxy OAuth
	4.5.4 Déclaration des règles Ingress
	4.6 Tests de connexion
	4.7 Restriction des accès
	4.7.1 Mécanisme d’autorisation
	4.7.2 Restriction par domaine e-mail
	4.7.3 Restriction par organisation GitHub
