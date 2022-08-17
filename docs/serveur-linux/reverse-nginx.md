# Comment faire un reverse proxy Nginx

Un serveur proxy est un serveur intermédiaire ou intermédiaire qui transfère les demandes de contenu de plusieurs clients vers différents serveurs sur Internet. Un serveur proxy inverse (reverse proxy) est un type de serveur proxy qui se trouve généralement derrière le pare-feu dans un réseau privé et dirige les demandes des clients vers le serveur principal approprié. Un proxy inverse fournit un niveau supplémentaire d'abstraction et de contrôle pour assurer la fluidité du trafic réseau entre les clients et les serveurs.

Dans ce tutoriel, nous allons voir comment mettre en place un reverse proxy sous Linux avec Nginx.

## Etape 1 : installer Nginx

### Debian, Ubuntu

```
sudo apt update
sudo apt install nginx
sudo systemctl enable --now nginx
```

### CentOS, Almalinux, Rocky...etc

```
sudo dnf install nginx
sudo systemctl enable --now nginx
```

## Etape 2 : Générer un certificat SSL si nécessaire

### Installation de certbot

#### Debian, Ubuntu

```
sudo apt update && sudo apt install python3-certbot-nginx
```

#### CentOS, Almalinux, Rocky...etc

```
sudo dnf install certbot python3-certbot-nginx
```

### Génération du certificat

```
certbot certonly -d <nom_domaine>
```

**Facultatif :** Si vous voulez activer le renouvellement automatique du certifcat SSL, ajoutez simplement la ligne suivante à cron (commande : `export VISUAL=nano;crontab -e`)

```
@daily certbot renew --quiet --nginx
``` 

## Ajout du fichier de configuration du reverse proxy

Sous Debian/Ubuntu, le fichier sera à mettre dans le dossier `/etc/nginx/sites-enabled/` alors que sous CentOS et dérivées, il sera à mettre dans le dossier `/etc/nginx/conf.d/`.

Nommez le comme vous voulez, je vous recommande : `<nom_domaine>.conf`

N'oubliez pas de remplacer les valeurs entre <>

### Configuration sans SSL

```
server {
        listen 80;
        listen [::]:80;
        server_name  <nom_domaine>;
        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;
        location / {
            proxy_pass http://localhost:<port>;    
        }
}
```

### Configuration avec SSL

```
server {
        listen 80;
        listen [::]:80;
        server_name  <nom_domaine>;
        return 302 https://$server_name$request_uri;
}

server {

        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        ssl_certificate         /etc/letsencrypt/live/<nom_domaine>/fullchain.pem;
        ssl_certificate_key     /etc/letsencrypt/live/<nom_domaine>/privkey.pem;
        server_name  <nom_domaine>;
        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;
        location / {
            proxy_pass http://localhost:<port>;    
        }
}
```

## Redémarrage de Nginx

Et voilà, vous venez de mettre en place votre reverse proxy, pour l'activer, vérifiez votre fichier de configuration via le commande `nginx -t` puis redémarrez le service via la commande `sudo systemctl restart nginx`