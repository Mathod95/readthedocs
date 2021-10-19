Installation
++++++++++++

Installing Ansible via PPA on Debian
====================================

Debian users may use the same source as the Ubuntu PPA (using the following table).

.. list-table::
  :header-rows: 1

  * - Debian
    -
    - Ubuntu
  * - Debian 11 (Bullseye)
    - ->
    - Ubuntu 20.04 (Focal)
  * - Debian 10 (Buster)
    - ->
    - Ubuntu 18.04 (Bionic)
  * - Debian 9 (Stretch)
    - ->
    - Ubuntu 16.04 (Xenial)
  * - Debian 8 (Jessie)
    - ->
    - Ubuntu 14.04 (Trusty)

.. note::

    As of Ansible 4.0.0, new releases will only be generated for Ubuntu 18.04 (Bionic) or later releases.

Add the following line to ``/etc/apt/sources.list`` or ``/etc/apt/sources.list.d/ansible.list``:

.. code-block:: bash

    echo -e "deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main" | sudo tee -a /etc/apt/sources.list.d/ansible.list

.. warning::
    On Debian you should probably need to install gnupg gnupg2 gnupg1

    .. code-block:: bash
        
        sudo apt install gnupg gnupg2 gnupg1

Then run these commands:

.. code-block:: bash

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
    sudo apt update
    sudo apt install ansible

.. note::
    To check the version of Ansible use the command ``ansible --version``

    .. code-block:: bash

        mathod@ANSIBLE:/etc/apt/sources.list.d$ ansible --version
        ansible [core 2.11.6] 
        config file = /etc/ansible/ansible.cfg
        configured module search path = ['/home/mathod/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
        ansible python module location = /usr/lib/python3/dist-packages/ansible
        ansible collection location = /home/mathod/.ansible/collections:/usr/share/ansible/collections
        executable location = /usr/bin/ansible
        python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]
        jinja version = 2.11.3
        libyaml = True

Upgrade Ansible via PPA
-----------------------

Installing Ansible via PIP
==========================

Upgrade Ansible via PIP
-----------------------

Autre
~~~~~