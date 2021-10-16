><font color="green"> Some green text </font>



#!/bin/bash
# template-create.sh
# Mathias Felix
# 20211004

apt-get install libguestfs-tools

wget https://cloud.debian.org/images/cloud/bullseye/daily/latest/debian-11-generic-amd64-daily.raw
virt-customize -a debian-11-generic-amd64-daily.raw --install qemu-guest-agent

DATE=$(date +"%Y%m%d%H%M")
qm create 100 --name "DEBIAN11-$DATE" --memory 1024 --balloon 512 --net0 virtio,bridge=vmbr0 --cores 2 --sockets 1
qm importdisk 100 debian-11-generic-amd64-daily.raw shared-cephfs
qm set 100 --scsihw virtio-scsi-pci --scsi0 shared-cephfs:vm-100-disk-0
qm set 100 --serial0 socket
qm set 100 --boot c --bootdisk scsi0
qm set 100 --tablet 0
qm set 100 --ostype l26
qm set 100 --agent 1,fstrim_cloned_disks=1
qm set 100 --scsi1 shared-cephfs:cloudinit
qm resize 100 scsi0 +8G
qm set 100 --ciuser mathod
qm set 100 --cipassword mathod
qm set 100 --ipconfig0 ip=91.121.57.85/32,gw=193.70.34.254
qm set 100 --nameserver 8.8.8.8
qm set 100 --onboot 1

02:00:00:2f:90:3d
qm start 100
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDY4OigF88Sji4FmVh7vYOG3hgEpiN7lTcw/9dkx2dlThjxUmS/waW+hwsl6cEXDTc034b2pdhV17Z7D1WtfrUKW4qrKurHw88e5OOrpricAIxlX05ms8JTcsOQuk+QjYg01NRIYqbUB6XXtS0dPTNhM+Ht7EbE6ykdRTOHXhqtfIbmQQ4Uep0VmbTAlvQTWuhizGL2IUIQIHFkr5q1CHq6cL2pfCi4RAut4rTjiV90/DHbg9uzQ1wNxd7cu2HZ8EQG67dzl7/Hm/9T6BBwJiYTTsGJ2l408z+NNLPo4svBic4W1XOHwy0yWlnClh5Ltk+y6ZFkx3TXmUPUWcPRaT+t ksaliba@evina-ksa

add-apt-repository -y ppa:wireguard/wireguard
apt-get update
apt-get install -y wireguard

# Remove dnsmasq because it will run inside the container.
apt-get remove -y dnsmasq

# Set DNS server.
echo nameserver 1.1.1.1 >/etc/resolv.conf

# Load modules.
modprobe wireguard
modprobe iptable_nat
modprobe ip6table_nat

# Enable IP forwarding
sysctl -w net.ipv4.ip_forward=1
sysctl -w net.ipv6.conf.all.forwarding=1

[Interface]
Address = 10.0.0.1/26
PrivateKey = aPE2ihPMG5LtcQY6VOzUOo/Sbdy7XFc//jD6wI2DT3s=
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t
nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t
nat -D POSTROUTING -o eth0 -j MASQUERADE
ListenPort = 51820
SaveConfig = true

#Mathias
[Peer]
PublicKey = Lv3C2SaSO5LPxtIWMX3WKfmwbaO5n4C5ln29NY9DyAE=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.2/32

#Julien
[Peer]
PublicKey = SBD+qyNXydkNOjsA+Y/YVOsN7RPknJTv/lh0RFQBQyU=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.3/32

#Kenny
[Peer]
PublicKey = ErOeGYxzqqDlmvETMAybwdb0FeTWlOgMKNDUCg7TUUU=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.4/32






client1-private.key = YMVhlQBaRhRfV7HQYp7d6FcgN+KkgM1rW2c1V/dB6UM=
client1-public.key 	= Lv3C2SaSO5LPxtIWMX3WKfmwbaO5n4C5ln29NY9DyAE=
partage-shared.key 	= 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
server-private.key 	= aPE2ihPMG5LtcQY6VOzUOo/Sbdy7XFc//jD6wI2DT3s=
server-public.key 	= 6SuIUADy6NofxEftdf55iwNXWjHy3cFOW+uFxIn3KQ4=


# Enable IPv4 Forward
'echo 0 > /proc/sys/net/ipv4/ip_forward'

# Désactivation de l'IPv6
# désactivation de ipv6 pour toutes les interfaces
'echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf'
# désactivation de l’auto configuration pour toutes les interfaces
'echo "net.ipv6.conf.all.autoconf = 0" >> /etc/sysctl.conf'
# désactivation de ipv6 pour les nouvelles interfaces (ex:si ajout de carte réseau)
'echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf'
# désactivation de l’auto configuration pour les nouvelles interfaces
'echo "net.ipv6.conf.default.autoconf = 0" >> /etc/sysctl.conf'


sysctl net.ipv6.ip_forward




[Interface]
Address = 10.0.0.1/26
SaveConfig = true
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
ListenPort = 51820
PrivateKey = aPE2ihPMG5LtcQY6VOzUOo/Sbdy7XFc//jD6wI2DT3s=

[Peer]
PublicKey = Lv3C2SaSO5LPxtIWMX3WKfmwbaO5n4C5ln29NY9DyAE=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.2/32

[Peer]
PublicKey = SBD+qyNXydkNOjsA+Y/YVOsN7RPknJTv/lh0RFQBQyU=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.3/32

[Peer]
PublicKey = ErOeGYxzqqDlmvETMAybwdb0FeTWlOgMKNDUCg7TUUU=
PresharedKey = 59+qZU9FLYAvFURznYR3XhATB+RnY7onU8DFua7qyXY=
AllowedIPs = 10.0.0.4/32

PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -A FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -D FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Ma commande qui marche
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Commande à tester
PostUp = iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Mix des deux
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE