- modification du fichier config mysql
```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

- Vérouiller l'édition des tables SQL
```bash
sudo mysql
```
```sql
flush tables with read lock;
```

- Dévérouiller l'édition des tables sql
```bash
sudo mysql
```
```sql
unlock tables;
```

- Créer un compte réplicateur
```sql
create user 'replicateur'@'%' identified by 'Btssio2017';
```

- Donner tout les droit au compte réplicateur
```sql
grant replication slave on *.* to 'replicateur'@'%';
```

- Voir le status du master
```bash
sudo mysql
```
```sql
slow master status;
```

- Recréer le fichier log
```bash
sudo mkdir -m 2750 /var/log/mysql
sudo chown mysql /var/log/mysql
```

- Arreter le slave
```bash
sudo mysql
```
```sql
stop slave;
```

- Démarrer le slave
```bash
sudo mysql
```
```sql
start slave;
```

- Paraméter le serveur esclave pour reconnaitre le master
```bash
sudo mysql
```
```sql
change master to master_host='172.16.0.10', master_user='replicateur', master_password='Btssio2017', master_log_file='mysql-bin.000002', master_log_pos=328;
```

- Voir le status du slave
```bash
sudo mysql
```
```sql
show slave status;
```

