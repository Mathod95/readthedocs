# CaseStudy_1
## Installation Ansible sur Debian 11
### Context and prerequisites
#### Les point que vous allez travailler et mettre en œuvre :
- Installation d'Ansible via repo PPA
- Installation d'Ansible via Python pip3
#### Connaissance & prérequis nécessaire :
- Installation de package sous Debian 11
#### Matériel à disposition :
- Serveur Debian 11 ANSIBLE 192.168.1.110
#### Connaissance acquise à la fin de ce chapitre :
- Installation de Ansible sous Debian 10

## Installation de Ansible via repository PPA

## Installation de Ansible via python3-pip
```
sudo apt install python3 python3-pip
sudo pip3 install ansible
ansible --version
```

```
mathod@ANSIBLE:~$ ansible --version
ansible [core 2.11.6] 
  config file = /home/mathod/ansible.cfg
  configured module search path = ['/home/mathod/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.9/dist-packages/ansible
  ansible collection location = /home/mathod/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]
  jinja version = 2.11.3
  libyaml = True
```
Le fichier de configuration se trouve ici
https://github.com/ansible/ansible/blob/stable-2.11/examples/ansible.cfg

---