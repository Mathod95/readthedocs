# Installing Ansible on Debian 11
Debian users may use the same source as the Ubuntu PPA (using the following table).

Debian | Ubuntu
------ | ------
Debian 11 (Bullseye) | Ubuntu 20.04 (Focal)
Debian 10 (Buster) | Ubuntu 18.04 (Bionic)

Add the following line to /etc/apt/sources.list.d/ansible.list:

```
echo -e "deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main" | sudo tee -a /etc/apt/sources.list.d/ansible.list
```

Then run these commands:

```
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
$ sudo apt update
$ sudo apt install ansible
```

Finally run `ansible --version` to confirm the installation:

```
mathod@MATHOD:~$ sudo ansible --version
ansible [core 2.11.5]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]
  jinja version = 2.11.3
  libyaml = True
```

---

[Documentation Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-debian)