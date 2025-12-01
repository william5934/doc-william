## Création du fichier de configuration ip
```bash
sudo nano /etc/netplan/01-netcfg.yaml
```
## contenue du fichier de configuration
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: false
      addresses:
        - 172.16.0.6/24
      routes:
        - to: default
          via: 172.16.0.254
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4