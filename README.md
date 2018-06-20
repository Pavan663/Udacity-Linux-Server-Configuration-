# Udacity-Linux-Server-Configuration
## About Project:
#### This project is about configuring the linus server
## About the server:
    Server Ip Address: 13.126.254.36
    Hosted url: http://13.126.254.36.xip.io/
## Process for database
####  install postgres:
    sudo apt-get install postgresql
####  login into postgres:
    sudo su - postgres
#### enter database shell:
    psql
#### create user:
    CREATE USER catalog WITH PASSWORD 'password';
#### Alter permissions:
      ALTER USER catalog CREATEDB;
#### Database name with user:
      CREATE DATABASE catalog WITH user catalog;
#### Connect to database:
     \c catalog
#### Revoke from permissions:
      REVOKE ALL ON SCHEMA public FROM public;
#### Grant permissions:
      GRANT ALL ON SCHEMA public TO catalog;
#### To get out of database and postgres:
      \q
      exit
#### Now change the database connection in both myproject.py and init.py as:
     engine = create_engine('postgresql://catalog:password@localhost/catalog')     
## Process to create grader user:
#### Grader key : -----BEGIN RSA PRIVATE KEY-----
    MIIEpAIBAAKCAQEA00JmLcBHfQpsV+dV5ZHGIxkXCudBh6QIt42+RXOT3g+vc5aV
    hWfHWO0G3DZz1UhkUcu/9/9hXW7e0Q6GXileTLg7zKZym2h1bnbKZl64vSJ1J1lg
    QIg48cxpAfx29oQ0y7atZPUjX9L0gMwmg0OGtQkPYrA75LVVR04TklryGIyQjMbv
    4qKtPq4z7g6h90IhgC5XVfSnRp7IiWZmgko9woZ36sEGUJ5lLFkQZsnB5q3AJgZ5
    sCK+kWvHeRuENk9ZhQgTzWd+U0r3AEtBkR8GHE0ULgvJuYyoIq1WZV/8Ji2MqYCQ
    otqqfpnTAlyXoQh8+pteFr9Md/ZPr8qeLuSUwwIDAQABAoIBAQCdBG75dj4sG8En
    HJPlSxGfKJjNy9ASxsKL2tgeuqael73qBXQgcV/jIljE99vkHCgj+3I1GyT80tjd
    PRR1i/3Au/YGR3hLNbqCXdxVdfWM7b1xf6ZgkF7yqOErTsAEvYKYHrCFpwWhxSNh
    T1sYmOnYSGGdEiuR84zssIUvdFUYFJfwfCFIbgH7jTpbAPfQChgn8CKAhoi7QHph
    EwbqftpEL1tmIOHCYv9DmkWTDd9SHeBTIY5GHjS6xEsmtI/FplmjtRFyJQYmFMvK
    JWuD0AKxPUu4agsVf0qtDE8zNxXQ56ZT46A16Xpy4s92urqJfTbr1T40nuFizvur
    S1RJhJhxAoGBAOk+Eyu/ExLL295IrMJKvsFFCBQMLcylLJp+uFhcjf4keG9nZhYq
    rsOccEAqVF4nf5WwyPZg9NJJem7j39po+9H6gkgoVzZHH4CJ4rzXBozQgM1gkZxD
    eIWAxT9a67HDo/XhIM+/1bLHuQdnj3hJv92TKFNp/Cf1hws5fzKwRQltAoGBAOff
    Ow6Q0Wa0Shl6kDPnvoV2JbFjsSGdI/0y1fSuad5J8j5tfZABlZrHfrpzNCe9DQAv
    62x1renLlwt6ZkXscwOiygyQ5pJNo5XVXtmWecXylu1f/nP5A7n10p/2StQ6i5Gy
    nboWpulgDI/kns2wW1dIBSLyJsSDMINcDa3rvujvAoGBAL3lARyzwyahfM+74ZOJ
    4UZfGpWf2MXtkKP0GcgvCpfoP3mL+GyBsammuykyjV/ezpwjw2n8RDbVBe40brNW
    l/c7+kgfN+oD+9zd5hETC80nkEYlokdUE1K2JWFQd+ZRvzLXaKxbpfOZccZahU9M
    0/3k6ocHGfm6h4kW9b1iD8L9AoGAUOv/WF4CNq3FDo9PtE20mC9biEUalHibDsqn
    EPWtzP5RpKfholhrNdFZ0QhTs2qvFtmid/+56lY7KK5W8yBKI4K0sR4A2h5ucOQ+
    bgGuDf9T3RQbYa4ONuAr2dfC1b545yhHE6LELb5vo+hN48sglZ107XVFQl/mlnGR
    9JjJz9ECgYAmSJaWGEObi28lSHcGStDN/OU7s2/TLf2o8S473unLAJGgVwwhJaZf
    mAZj3QmmHbuJyUXnZWeHkkKJm0IcaFVZa0aNnkh+RE1ZoNRpp9Rc5D374dgtBqZ6
    GJYzKWPdosCzgGSBCoGJAVXDHk9T1fPFBXJZ9PnbCQdbpN6a64Jw8w==
    -----END RSA PRIVATE KEY-----
#### Grader password: 
      1234
#### sudo adduser grader
#### It adds new user
     sudo nano/etc/sudoers
####  In the above file we include the following:
     grader  ALL=(ALL:ALL) ALL
#### The above sentence gives permission to grader
##  To Create ssh key pair for grader:
#### On your local machine in terminal in ubuntu for example/command prompt for example windows
    ssh-keygen
#### The above command creates keys in .ssh folder
     su - grader
#### create .ssh directory and new file authorized_keys
     mkdir .ssh
     sudo nano .ssh/authorized_keys
#### Now place the public key with .pub extension to authorized_keys and save the file
     chmod 700 .ssh
     chmod 644 .ssh/authorized_keys
     service ssh restart
#### Logging in to grader with private key generated
     ssh -i .ssh/id_rsa grader@ipaddress 
#### Change the port 22 to 2200 
     sudo nano /etc/ssh/sshd_config
#### Restart the ssh server
     service ssh restart
#### Now get login using command:
     ssh -i .ssh/id_rsa grader@ipaddress
#### To change the existing root:
     sudo nano /etc/ssh/sshd_config
#### Security for firewalls:
     sudo ufw allow 2200/tcp
     sudo ufw allow 80/tcp
     sudo ufw allow 123/udp
     sudo ufw enable
## To get latest versions following update command:
    sudo get-apt update
## Next:
     check status:  sudo ufw status
     get time and date : sudo dpkg-reconfigure tzdata
     install apache2 : sudo apt-get install apache2
     mod_gsi : sudo apt-get install python-setuptools libapache2-mod-wsgi
     enable :  sudo a2enmod wsgi
#### create FlaskApp directory:
     sudo mkdir FlaskApp
     cd FlaskApp
#### install git:
     sudo apt-get install git
#### git clone:
     sudo git clone https://github.com/swathigollapudi/catalog_project.git  
#### change main file name:
       sudo mv myfinalproject.py __init__.py
#### Open main file and add json file as following:
      sudo nano __init__.py
      PROJECT_ROOT = os.path.realpath(os.path.dirname(__file__))
      json_url = os.path.join(PROJECT_ROOT, 'client_secrets.json')
#### save and exit:
     ctrl+o
     ctrl+x
#### create wsgi file:
      sudo nano mv project.py FlaskApp.wsgi
      #!/usr/bin/python
      import sys
      import logging
      logging.basicConfig(stream=sys.stderr)
      sys.path.insert(0,"/var/www/FlaskApp/")
      from FlaskApp import app as application
      application.secret_key = 'Add your secret key'
#### Creating virtual host file:
        sudo nano /etc/apache2/sites-available/FlaskApp.conf
        <VirtualHost *:80>
        ServerName mywebsite.com
        ServerAdmin admin@mywebsite.com
        WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
        <Directory /var/www/FlaskApp/FlaskApp/>
	       Order allow,deny
	       Allow from all
        </Directory>
        Alias /static /var/www/FlaskApp/FlaskApp/static
        <Directory /var/www/FlaskApp/FlaskApp/static/>
	       Order allow,deny
	       Allow from all
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>
#### To install some required sofwares:
      pip install sqlalchemy
      pip install flask
      pip install oauth2client
      pip install pyscopg2
      pip install requests
#### Now our appilication is ready
### setting oauth2 client details:
   ## Login to your developer console and select the project and edit OAuth details as following:
      redirect URI
      http://ip.xip.io\login
      http://ip.xip.io\gconnect
      http://ip.xip.io\callback
## Finally restart the server:
    sudo service apache2 restart
