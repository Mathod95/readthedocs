evina@ANSIBLE:~$ ansible -i hosts.ini DEBIAN -m ansible.builtin.setup



sudo apt remove ntp
sudo vim /etc/systemd/timesyncd.conf (uncomment NTP)
timedatectl set-ntp true
sudo systemctl restart systemd-timesyncd.service
systemctl status systemd-timesyncd.service

