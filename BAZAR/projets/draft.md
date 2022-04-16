evina@ANSIBLE:~$ ansible -i hosts.ini DEBIAN -m ansible.builtin.setup



sudo apt remove ntp
sudo vim /etc/systemd/timesyncd.conf (uncomment NTP)
timedatectl set-ntp true
sudo systemctl restart systemd-timesyncd.service
systemctl status systemd-timesyncd.service

><font color="green"> Some green text </font>



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