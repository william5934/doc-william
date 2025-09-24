### Sur le serveur maitre
# Modifier le fichier de config 50-server.cnf
```bash
cp /tc/mysql/maridb.conf.d/50-srvr.cnf /tc/mysql/maridb.conf.d/50-srvr.cnf.sav
sudo nano /tc/mysql/maridb.conf.d/50-srvr.cnf
```
- Modifier les option suivante
```bash
bind-address = <ip de la machine>
log_error = /var/log/mysql/error.log
server-id = 100
log_bin = /var/log/mysql/mysql-bin.log
expire_logs_days = 10
max_bindlog_size = 100M
binlog_do_db = <nom de la base de données>
```
# Créer le dossier d'erreur mysql
```bash
sudo mkdir -m 2750 /var/log/mysql
```

# Redémarrer le service mysql
```bash
sudo systemctl restart mariadb.service
```
# Vérifier si il n'y a pas d'erreur
```bash
systemctl status mariadb.service
```

### Sur le serveur esclave
# Modifier le fichier de config 50-server.cnf
```bash
cp /tc/mysql/maridb.conf.d/50-srvr.cnf /tc/mysql/maridb.conf.d/50-srvr.cnf.sav
sudo nano /tc/mysql/maridb.conf.d/50-srvr.cnf
```
- Modifier les option suivante
```bash
log_error = /var/log/mysql/error.log
server-id = 101
expire_log_days = 10
max_binlog_size = 100M
master-retry-count = 20
binlog_do_db = <nom de la base de données>
```
# Créer le dossier d'erreur mysql
```bash
sudo mkdir -m 2750 /var/log/mysql
```

# Redémarrer le service mysql
```bash
sudo systemctl restart mariadb.service
```
# Vérifier si il n'y a pas d'erreur
```bash
systemctl status mariadb.service
```
### Sur la machine master
# Bloquer l'écriture dans la base de données
```bash
sudo mysql
```
```sql
flush tables with read lock;
```

# Création d'un utilisateur réplicateur
- Créer un compte réplicateur
```sql
create user 'replicateur'@'%' identified by 'Btssio2017';
```

# Donner tout les droit au compte réplicateur
```sql
grant replication slave on *.* to 'replicateur'@'%';
``