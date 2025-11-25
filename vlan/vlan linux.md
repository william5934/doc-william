# Installation vlan
```bash
apt-get update
apt-get upgrade -y
apt-get install vlan
```

# Activation du module
```bash
echo "8021q" | sudo tee -a /etc/modules
modprobe 8021q
```

# Vérification du module
```bash
lsmod | grep 8021q
```
- Vous devriez voir cela
```bash
8021q                  40960  0
garp                   16384  1 8021q
mrp                    20480  1 8021q
```