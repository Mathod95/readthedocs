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

Now you need to copy the content of your public key to ~/.ssh/authorized_keys file on remote machine.
Create .ssh directory and authorized_keys file in the user home directory ( if root then /home/root), if it doesn't exist.
To do so you can do manually or by using ssh-copy-id command.
By using ssh-copy-id
If you don't want to copy it manually, we can use ssh-copy-id command which will do the same as follows:

```
sudo ssh-copy-id -i ~/.ssh/id_rsa.pub evina@MASTER01
```
## 3) Verify the passwordless ssh
Now we have copied public key to the server, we should be good to login without any password.
We can verify by running the following ssh command using the user (tom):

```
[tom@centos02 ~]$ ssh tom@45.33.3.15 
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.4.0-26-generic x86_64)
Last login: Fri May 29 03:14:32 2020 from 104.237.141.158
hostname
ubuntu01
```

You can see from the above output that it didn't prompt for any password.


## Disable password authentication
If all user accounts on the server are authenticated using public keys (including root), you can disable authentication by a password.
To enable authentication by public key and disable authentication by password, you edit /etc/ssh/sshd_config file.
Modify the below lines on sshd_config:

```
$ vi /etc/ssh/sshd_config
RSAAuthentication yes
PubkeyAuthentication yes
PasswordAuthentication no
UsePAM no
ChallengeResponseAuthentication no
```

After making the changes restart sshd service:
```
$ sudo systemctl reload sshd
```

Once users are authenticated using keys, you may consider disabling the 'root' login for ssh (set PermitRootLogin no).
Keys with passphrase

```
$ ssh-agent $SHELL
$ ssh-add -L
The agent has no identities.
$ ssh-add 
Enter passphrase for /home/tom/.ssh/id_rsa:
Identity added: /home/tom/.ssh/id_rsa (tom@linoxide.com)
```

Now try to login again, see that you are not prompted for the passphrase.

## Set Permission
Just make sure .ssh directory and authorized_keys files on the remote server have appropriate permissions. To protect the public key set permissions for the access of the key as follows:

```
$ sudo chmod 700 .ssh
$ sudo chmod 600 .ssh/authorized_keys
```

## Conclusion
In this tutorial, we have explained how to set up passwordless login between two Linux systems. In case you want to revoke access, then remove the line for the public key from the authorized_keys file.
It's best practice to enable SSH public key authentication rather than using passwords over the networks. However, it's equally important to renew your SSH keys on frequent time interval for more safety.
Note that the DSA and RSA 1024 bit keys are deprecated. It's advised to upgrade keys to use the latest ed25519 or ecdsa algorithms which have high-security signatures.
Pour ajouter la clé à l’agent, il faut passer par la commande ssh-add suivie du chemin vers la clé SSH. La commande demandera alors de saisir la passphrase. Ci-dessous un exemple d’ajout de clé SSH :

```
$ ssh-add .ssh/id_rsa
```

```
Enter passphrase for .ssh/id_rsa:  
Identity added: .ssh/id_rsa (.ssh/id_rsa)
```

Dans le cas où vous obtenez le message Error connecting to agent: No such file or directory, il vous faut lancer un agent SSH avec la commande eval $(ssh-agent). Ci-dessous un exemple de lancement de cet agent :

```
$ eval $(ssh-agent)
```


Cette commande doit retourner la sortie suivante :

```
Agent pid 20811
```
Dans le cas où Ansible est lancé depuis une application tierce, ces clés devront être gérées par un mécanisme externe. Dans le cas de Jenkins, le plugin SSH Agent Plugin peut être utilisé. Dans d’autres cas, il n’y aura pas forcément de solutions miracles. Il faudra alors se passer de ce mécanisme.
Pour ajouter votre clé SSH à l'agent utiliser la commande suivante puis indiquer le passphrase de la clé

```
evina@ANSIBLE:~$ ssh-add
Enter passphrase for /home/evina/.ssh/id_rsa: 
Identity added: /home/evina/.ssh/id_rsa (ANSIBLE)
```

---