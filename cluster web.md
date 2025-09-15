# Mise en place d'un cluster web

- Installation de corosync, pacemaker et crmsh
```bash
apt install corosync pacemaker crmsh
```

- Création de la clé  authkey pour le chiffrement des échanges.
```bash
corosync-keygen
ls -l /etc/corosync/
```

- Cloner la serveur web et changer son nom et son ip
- Visualiser l'état du cluster

- Désactiver le stonight (shot the other node in the head)
```bash
crm configure property stonith-enabled=false
```

- Visualiser l'état du cluster
```bash
crm status
crm configure show
```