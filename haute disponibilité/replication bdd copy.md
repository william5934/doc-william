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
# Récupérer les info du master
```bash
sudo mysql
```
```sql
show master status;
```
- Récupérer le **file** (ex : mysql-bin.000001) et la **Position** (ex : 3921)

### Sur la machine slave
# Configuration de mysql pour se connecter au master
```bash
sudo mysql
```
```sql
change master to master_host='ip du master', master_user='replicateur', master_password='Btssio2017', master_log_file='mysql-bin.000002', master_log_pos=328;
```
### Sur le serveur maitre
# Dévérouillage des tables
```bash
sudo mysql
```
```sql
unlock tables;
```

### Sur la machine slave
# Vérifier le status de l'esclave
```bash
sudo mysql
```
```sql
show slave status \G;
```
- Vous devez voir s'afficher **Waiting for master to send evant** a l'onglet **Slave_IO_State**

