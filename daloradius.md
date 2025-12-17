Rasberry Pi 5 - Rasberry Pi os

Install FreeRADIUS and Daloradius

```
sudo apt update && sudo apt -y upgrade
```

```
sudo apt -y install apache2
sudo systemctl enable --now apache2

```

```
sudo apt -y install vim php libapache2-mod-php php-{gd,common,mail,mail-mime,mysql,pear,db,mbstring,xml,curl,zip}
```

3. Install MariaDB and Create database
```
sudo apt update && sudo apt install mariadb-server
```


```
database name: radius
database user: radius
database user password: Str0ngR@diusPass
```

```
sudo mysql -u root -p
CREATE DATABASE radius;
GRANT ALL ON radius.* TO radius@localhost IDENTIFIED BY "Str0ngR@diusPass";
FLUSH PRIVILEGES;
QUIT
```

```
systemctl status apache2
sudo ufw allow http
sudo apt install ufw
sudo ufw allow http
sudo ufw allow https
```

```
sudo apt -y install freeradius freeradius-mysql freeradius-utils
sudo systemctl enable --now freeradius.service 

```


```
sudo ln -s /etc/freeradius/3.0/mods-available/sql /etc/freeradius/3.0/mods-enabled/
```

```
sudo vim /etc/freeradius/3.0/mods-available/sql
```

```
sql {
driver = "rlm_sql_mysql"
dialect = "mysql"

# Connection info:
server = "localhost"
port = 3306
login = "radius"
password = "Str0ngR@diusPass"

# Database table configuration for everything except Oracle
radius_db = "radius"
}

# Set to ‘yes’ to read radius clients from the database (‘nas’ table)
# Clients will ONLY be read on server startup.
read_clients = yes

# Table to keep radius client info
client_table = "nas"
```

```
        mysql {
                # If any of the files below are set, TLS encryption is enabled
#               tls {
#                       ca_file = "/etc/ssl/certs/my_ca.crt"
#                       ca_path = "/etc/ssl/certs/"
#                       certificate_file = "/etc/ssl/certs/private/client.crt"
#                       private_key_file = "/etc/ssl/certs/private/client.key"
#                       cipher = "DHE-RSA-AES256-SHA:AES128-SHA"
#
#                       tls_required = yes
#                       tls_check_cert = no
#                       tls_check_cert_cn = no
#               }

                # If yes, (or auto and libmysqlclient reports warnings are
                # available), will retrieve and log additional warnings from
                # the server if an error has occured. Defaults to 'auto'
                warnings = auto
        }
```

```
sudo chgrp -h freerad /etc/freeradius/3.0/mods-available/sql
sudo chown -R freerad:freerad /etc/freeradius/3.0/mods-enabled/sql
sudo systemctl restart freeradius
```

5. Install and Configure Daloradius
```
sudo apt -y install git
git clone https://github.com/lirantal/daloradius.git
```

```
sudo mariadb -u root -p radius < daloradius/contrib/db/fr3-mariadb-freeradius.sql
sudo mariadb -u root -p radius < daloradius/contrib/db/mariadb-daloradius.sql

```

```
sudo mv daloradius /var/www/
```

```
sudo mv daloradius /var/www/
cd /var/www/daloradius/app/common/includes/
sudo cp daloradius.conf.php.sample daloradius.conf.php
sudo chown www-data:www-data daloradius.conf.php
sudo vim daloradius.conf.php

```

```
sudo vim daloradius.conf.php
```

```
$configValues['CONFIG_DB_HOST'] = 'localhost';
$configValues['CONFIG_DB_PORT'] = '3306';
$configValues['CONFIG_DB_USER'] = 'radius';
$configValues['CONFIG_DB_PASS'] = 'Str0ngR@diusPass';
$configValues['CONFIG_DB_NAME'] = 'radius';
```

```
cd /var/www/daloradius/
sudo mkdir -p var/{log,backup}
sudo chown -R www-data:www-data var
```

```
sudo vim daloradius.conf.php

sudo tee /etc/apache2/ports.conf<<EOF
Listen 80
Listen 8000

<IfModule ssl_module>
    Listen 443
</IfModule>

<IfModule mod_gnutls.c>
    Listen 443
</IfModule>
EOF
```

```
sudo tee /etc/apache2/sites-available/operators.conf<<EOF
<VirtualHost *:8000>
    ServerAdmin operators@localhost
    DocumentRoot /var/www/daloradius/app/operators

    <Directory /var/www/daloradius/app/operators>
        Options -Indexes +FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    <Directory /var/www/daloradius>
        Require all denied
    </Directory>

    ErrorLog \${APACHE_LOG_DIR}/daloradius/operators/error.log
    CustomLog \${APACHE_LOG_DIR}/daloradius/operators/access.log combined
</VirtualHost>
EOF

```

```
sudo tee /etc/apache2/sites-available/users.conf<<EOF
<VirtualHost *:80>
    ServerAdmin users@localhost
    DocumentRoot /var/www/daloradius/app/users

    <Directory /var/www/daloradius/app/users>
        Options -Indexes +FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    <Directory /var/www/daloradius>
        Require all denied
    </Directory>

    ErrorLog \${APACHE_LOG_DIR}/daloradius/users/error.log
    CustomLog \${APACHE_LOG_DIR}/daloradius/users/access.log combined
</VirtualHost>
EOF

```

```
sudo a2ensite users.conf operators.conf
```

```
sudo mkdir -p /var/log/apache2/daloradius/{operators,users}
```

```
sudo a2dissite 000-default.conf
```

```
sudo systemctl restart apache2 freeradius
```

```
Access the service on the following URLS:

```

```
RADIUS management application: http://192.168.1.2:8000/

```
```
sudo vim /etc/freeradius/3.0/clients.conf
```
```
client wrt1200ac {
    ipaddr = 192.168.1.1
    secret = tprezo89!
    require_message_authenticator = no
}

client opnsense {
    ipaddr = 192.168.1.3
    secret = tprezo89!
    require_message_authenticator = no
}
```
