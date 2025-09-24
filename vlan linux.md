# Installation des packet requis
```bash
sudo apt update
sudo apt install vlan
```
# Charger le module noyau 8021q
```bash
sudo modprobe 8021q
echo "8021q" | sudo tee -a /etc/modules
```
# Création du vlan
1. modifier le fichier interface
```bash
sudo nano /etc/network/interfaces
```
```bash
auto eth0
iface eth0 inet manual
    up ip link set dev $IFACE up
    down ip link set dev $IFACE down

auto eth0.10
iface eth0.10 inet static
    address 192.168.10.100
    netmask 255.255.255.0
    gateway 192.168.10.1
    dns-nameservers 8.8.8.8 8.8.4.4
    vlan-raw-device eth0
```