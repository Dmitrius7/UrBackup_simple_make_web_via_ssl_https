# UrBackup_simple_make_web_via_ssl_https
Simple make UrBackup web interface accessible via SSL (nginx).
I use it with debian 10. If you use another OS change paths.

Official UrBackup documentation: https://www.urbackup.org/administration_manual.html#x1-200004.2


### How to use (step by step manual for debian)
This is step by step manual for debian. If you use another OS modify paths and commands.

    # Allow port 55416 at the ufw firewall (optionally, only if you use ufw firewall)
    sudo ufw allow 55416/tcp

    # Install nginx openssl 
    sudo apt update
    sudo apt install nginx openssl 

    # Create a Self-Signed SSL Certificate
    sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
    sudo openssl req -x509 -nodes -days 2562 -newkey rsa:2048 -subj "/O=Urb Security/OU=Urb/CN=Urb.local/CN=Urb" -keyout /etc/ssl/certs/urb-cert.key -out /etc/ssl/certs/urb-cert.crt

    Put these scripts to `/etc/nginx`;

    # Enable site at nginx
    sudo ln -s /etc/nginx/sites-available/urbackup.conf /etc/nginx/sites-enabled/urbackup.conf

    # Remove default site if you use nginx only for urbackup (optionally)
    sudo rm /etc/nginx/sites-enabled/default

    # restart nginx
    sudo service nginx restart

#### Open your UrBackup web interface by https
[https://IP_or_HOSTNAME:55416/](https://IP_or_HOSTNAME:55416/)

By default it use 55416. You can configure it at `/etc/nginx/sites-available/urbackup.conf`
