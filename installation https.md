# Mettre a jour la machine :
sudo apt update && sudo apt upgrade -y

# Installation openssl
sudo apt install openssl -y

# Modifier le fichier de configuration de openssl
sudo nano /etc/ssl/openssl.cnf

**Voici l'extrait qui nous intéresse :**
[ CA_default ]
dir = ./demoCA # Where everything is kept
certs = $dir/certs # Where the issued certs are kept
crl_dir = $dir/crl # Where the issued crl are kept
database = $dir/index.txt # database index file
...
new_certs_dir = $dir/newcerts # default place for new certs.
certificate = $dir/cacert.pem # The CA certificate
serial = $dir/serial # The current serial number
...
crl = $dir/crl.pem # The current CRL
private_key = $dir/private/cakey.pem # The private key

**Les modifications à faire sont :**