# Mémo SQL
- Créer une base de données (console sql)
```sql
create database gsb_valide;
```

- Créer un nouvel utilisateur (console sql)
```sql
create user 'userGsb'@'localhost' identified by 'secret';
```

- Créer un nouvel utilisateur (console bash)
```bash
mysql gsb_valide < nom_fichier.sql
```

- Donner des droits d'un utilisateur à une base (console sql)
```sql
grant all privileges on gsb_valide.* to 'userGsb'@'localhost';
flush privileges
```
- Afficher le contenu d'une table (console sql)
```sql
select * from Visiteur;
```

- Utilisé une base (console sql)
```sql
Use gsb_valide;
```
