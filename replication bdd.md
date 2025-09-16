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