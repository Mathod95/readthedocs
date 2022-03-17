•	Cycle de vie d’un container dans Kubernetes
o	1. Objectifs du chapitre et prérequis
o	2. Gestion des crashs d’application
	2.1 Consultation de l'état des pods
	2.2 Connexion au pod
	2.3 Container associé à MailHog
	2.4 Comportement en cas de crash
	2.5 État du container après redémarrage du pod
	2.6 Container vu depuis Docker (Minikube)
	2.7 Attention au nettoyage
o	3. État d’un container
	3.1 Pourquoi scruter l’état d’un container ?
	3.2 Readiness vs Liveness
	3.3 Utilisation et bonne pratique
	3.4 Structure des champs de surveillance
	3.5 Vérification de la présence d’un port
	3.5.1 Définition de la surveillance
	3.5.2 Test d’indisponibilité sur un pod non prêt
	3.5.3 État des pods en cas d’indisponibilité
	3.5.4 Test d’indisponibilité sur un pod en mauvaise santé
	3.5.5 État des pods en cas de problème sur un pod
	3.5.6 Attention à la consistance des tests
	3.5.7 Uniformisation des tests
	3.6 Surveillance HTTP
	3.6.1 Pourquoi privilégier ce type de surveillance ?
	3.6.2 Surveillance de l’application MailHog
	3.7 Point d’entrée de surveillance HTTP d’une application
	3.7.1 Un mot sur les frameworks modernes
	3.7.2 Présentation de l’application Flask
	3.7.3 Exemple de déclaration
	3.7.4 Déploiement de l’application Flask
	3.7.5 Consultation de l’état de l’application
	3.8 Lancement d’un shell
	3.8.1 Principe de fonctionnement
	3.8.2 Exemple de surveillance d’une base Postgres
	3.8.3 Déclaration de la commande
o	4. Définition de la capacité d’un pod
	4.1 Pourquoi définir une capacité ?
	4.2 Réservation et surallocation
	4.3 Allocation de ressources à un container
	4.4 Allocation de ressources à l’application MailHog
	4.5 Comportement en cas de saturation des ressources
	4.5.1 Demande trop importante de CPU
	4.5.2 Dépassement de la mémoire allouée
	4.6 Priorité d’un pod
	4.6.1 Présentation du mécanisme
	4.6.2 Consultation des types par défaut
	4.6.3 Consultation des priorités des pods
	4.6.4 Création d’une classe de priorité
	4.6.5 Affectation d’une classe de priorité personnalisée
	4.6.6 Remarque sur les classes de priorité par défaut
