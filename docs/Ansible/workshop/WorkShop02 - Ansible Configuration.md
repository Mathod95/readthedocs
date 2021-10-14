# CaseStudy_2
## Création et partage de clé ssh
### Context and prerequisites
#### Les point que vous allez travailler et mettre en œuvre :
- Générer une clé SSH
- Partager cette clé SSH sur des hosts afins de pouvoir les manager par la suite
- Configurer SSH afin d'y apporter des restriction/sécurité
#### Connaissance & prérequis nécessaire :
- SSH et son fonctionnement
#### Matériel à disposition :
- Serveur Debian 11 ANSIBLE
- Serveur Debian 11 PROD-CLIENTS111 192.168.1.111
- Serveur Debian 11 PROD-CLIENTS112 192.168.1.112
- Serveur Debian 11 PROD-CLIENTS113 192.168.1.113
- Serveur Debian 11 STAG-CLIENTS121 192.168.1.121
- Serveur Debian 11 STAG-CLIENTS122 192.168.1.122
- Serveur Debian 11 STAG-CLIENTS123 192.168.1.123
- Serveur Debian 11 TEST-CLIENTS124 192.168.1.131
- Serveur Debian 11 TEST-CLIENTS125 192.168.1.132
- Serveur Debian 11 TEST-CLIENTS126 192.168.1.133
#### Connaissance acquise à la fin de ce chapitre :
- Installation de Ansible sous Debian 10

## Génération de la clé SSH
Pour générer une paire de clé SSH + passphrase nous allons utiliser la commande ssh-keyygen suivante:

```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_<user> -C "ANSIBLE"
```

- -t rsa: Specifies the type of key to create.
- -b 4096: Specifies the number of bits in the key to create.
- -f ~/.ssh/id_rsa_<User>: Specifies the path to store your key.
- -C "FirstName NAME": Specifies a commentary inside the your key.

>Pour assurer l’intégralité de notre infrastructure lors de la génération de notre clé nous n’indiquons pas le passphrase dans la commande

Lors de l’exécution de la commande il vous seras demander de renseigner un passphrase et de le confirmer

Ce qui devrait nous donner l’output suivant:

```
[01:23:34]evina@BASTION:~$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -C "ANSIBLE"
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ~/.ssh/id_rsa
Your public key has been saved in ~/.ssh/id_rsa
The key fingerprint is:
SHA256:xePZw22e3DJHQWkGgvAArsd0ySJ8ZQzhgel08SjrG90 ANSIBLE
The key's randomart image is:
+---[RSA 4096]----+
|    o**=. .. ....|
|  .+o.B.+o  . .+ |
|  o+.B = .+   o. |
|   .O o  o = .  .|
|   o o  S o + o .|
|  . o .      = + |
|   o . E      * o|
|    o          + |
|   .             |
+----[SHA256]-----+
```
Pour obtenir votre clé publique utiliser la commande cat .ssh/id_rsa_ANSIBLE.pub

## Copie de la clé publique sur les serveurs à manager



---