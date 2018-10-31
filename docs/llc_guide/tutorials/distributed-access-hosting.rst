
.. _distributed-access-to-dex:

Distributed Access to the LocalCoin Decentralized  Exchange (DEX)
=================================================================
   
I hope to encourage and promote more access points and backup WebSocket (wss) gateways for LocalCoin. This is the logical progression from `Run your own decentralized
exchange <https://steemit.com/localcoin/@ihashfury/run-your-own-decentralised-exchange>`__
post.

.. contents:: Table of Contents
   :local:
   
-------

LocalCoin node setup
-------------------------------

`Run your own decentralized exchange <https://steemit.com/localcoin/@ihashfury/run-your-own-decentralised-exchange>`__

Once you have a full node setup, you can allow LocalCoin shareholders
secure access to your server to trade and check their accounts by
following these steps. 

* A DNS Alias (CNAME) is required to point to your server ip address. 
* See `dyn.com <http://dyn.com>`__ for DNS Alias setup. 
* You may have to wait a few days for the DNS to work through the internet. 
* Please change `yourdomain.com <http://yourdomain.com>`__ to your DNS alias in the examples below.


Create a New User
---------------------------

I recommend creating a new user on your server to run the Localcoin gui
and give the user sudo access. >You can use any name - I have used
localcoin in this example

::

    sudo adduser localcoin
    sudo gpasswd -a localcoin sudo
    sudo gpasswd -a localcoin users

Install Nginx
-------------------

Install Nginx web server

::

    # ssh into your new user localcoin
    ssh localcoin@yourdomain.com
    sudo apt-get install nginx
    # check version
    nginx -v
    # add user to web server group
    sudo gpasswd -a localcoin www-data
    # start nginx
    sudo service nginx start

This will start Nginx default web server. Check it by typing the ip
address of your server in a web browser or your alias
`yourdomain.com <http://yourdomain.com>`__

Configure Nginx
^^^^^^^^^^^^^^^^^^^^^^^^

To configure the web server, edit the default site and save as new DNS
alias name using http port 80 only until you setup
`letsencrypt.org <https://letsencrypt.org/>`__ SSL Certificate.

Create your web folder
^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo mkdir -p /var/www/yourdomain.com/public_html
    sudo chown -R localcoin:localcoin var/www/yourdomain.com/public_html
    sudo chmod 755 /var/www

Configure Nginx
^^^^^^^^^^^^^^^^^^^^^^

::

    # edit default setup and save as yourdomain.com
    sudo nano /etc/nginx/sites-available/default

Point to your new virtual host

::

    ###### yourdomain.com ######
    server {
        listen 80;
        server_name yourdomain.com;
        #rewrite ^ https://$server_name$request_uri? permanent;
        #rewrite ^ https://yourdomain.com$uri permanent;
        #
        root /var/www/yourdomain.com/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
    }

    CTRL+O to save as yourdomain.com (^O Write Out)

Update Virtual Host File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo cp yourdomain.com /etc/nginx/sites-available/yourdomain.com

Activate sim link and disable default web server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/yourdomain.com
    sudo rm /etc/nginx/sites-enabled/default

Link local folder to www root and add a simple index.html
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    ln -s /var/www/yourdomain.com/public_html ~/public_html
    nano ~/public_html/index.html

Add some text to index.html

::

    <html>
      <head>
        <title>yourdomain.com</title>
      </head>
      <body>
        <h1>yourdomain.com - Virtual Host</h1>
      </body>
    </html>

    CTRL+X to save as index.html (^X Exit) ###Restart Nginx

::

    sudo service nginx restart

Now you have setup a simple web server. DigitalOcean has a great
`article <https://www.digitalocean.com/community/articles/how-to-set-up-nginx-virtual-hosts-server-blocks-on-ubuntu-12-04-lts--3>`__
for more information on Virtual Host setup.

Install letsencrypt
---------------------------

::

    sudo apt-get install letsencrypt

Obtain your SSL certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo letsencrypt certonly --webroot -w /var/www/yourdomain.com/public_html -d yourdomain.com

Follow the instructions and add an email address

Check your certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo ls -l /etc/letsencrypt/live/yourdomain.com
    # and check it will update
    sudo letsencrypt renew --dry-run --agree-tos
    sudo letsencrypt renew

Setup a renew cronjob for your new SSL certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo crontab -e

Add this line to run the job every 6 hours on the 16th minute

::

    16 */6 * * *  /usr/bin/letsencrypt renew >> /var/log/letsencrypt-renew.log

    CTRL+X to save (^X Exit)

::

    # check your crontab
    sudo crontab -l

Generate Strong Diffie-Hellman Group cert
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048

Add SSL to Nginx settings
----------------------------------

Make a copy of yourdomain.com just in case.

::

    cp yourdomain.com alcap.io.no.ssl

Edit yourdomain.com
^^^^^^^^^^^^^^^^^^^

::

    nano yourdomain.com

::

    ###### yourdomain.com ######
    server {
        listen 80;
        server_name yourdomain.com;
        #rewrite ^ https://$server_name$request_uri? permanent;
        rewrite ^ https://yourdomain.com$uri permanent;
        #
        root /var/www/yourdomain.com/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
    }


    ###### yourdomain.com websockets


    upstream websockets {
        server localhost:8090;
    }


    ###### yourdomain.com ssl
    server {
        listen 443 ssl;
        #
        server_name yourdomain.com;
        #
        root /var/www/yourdomain.com/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
        #
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        ssl_dhparam /etc/ssl/certs/dhparam.pem;
        ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_stapling on;
        ssl_stapling_verify on;
        add_header Strict-Transport-Security max-age=15768000;
        #
        # Note: You should disable gzip for SSL traffic.
        # See: https://bugs.debian.org/773332
        #
        # Read up on ssl_ciphers to ensure a secure configuration.
        # See: https://bugs.debian.org/765782
        #
        # Self signed certs generated by the ssl-cert package
        # Don't use them in a production server!
        #
        # include snippets/snakeoil.conf;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
        location ~ /ws/? {
            access_log off;
            proxy_pass http://websockets;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
    }
    ###### yourdomain.com ######

    CTRL+X to save (^X Exit)

You have now setup an SSL secured web server with a WebSocket connected
to your local LocalCoin witness\_node (listening on port 8090 - see
`this
post <https://steemit.com/localcoin/@ihashfury/run-your-own-decentralised-exchange>`__
for more information) ###Update yourdomain.com www virtual host

::

    sudo cp yourdomain.com /etc/nginx/sites-available/yourdomain.com

Restart Nginx
^^^^^^^^^^^^^^

::

    sudo service nginx restart

Now you have setup an SSL web server. More information on SSL setup can
be found here. `DigitalOcean letsencrypt
SSL <https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04>`__
`LetsEncrypt <https://letsencrypt.org/>`__
`CertBot <https://certbot.eff.org/>`__

Install LocalCoin web gui
--------------------------

Install NVM (Node Version Manager)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash

exit bash (terminal) and reconnect

::

    ssh localcoin@yourdomain.com
    nvm install v5
    nvm use v5

Download LocalCoin gui
~~~~~~~~~~~~~~~~~~~~~~~~~

- https://github.com/localcoinis/localcoin-ui/releases

Setup light wallet
~~~~~~~~~~~~~~~~~~~

.. note:: Please refer localcoin-ui installation guide.

Build light wallet
~~~~~~~~~~~~~~~~~~~~~

::

    npm run build

You have now created another Access point to the LocalCoin Decentralised Exchange. **The more the merrier.** Please remember to check your firewall and SSH is up-to-date and configured correctly. DigitalOcean has
`firewall <https://www.digitalocean.com/community/tags/firewall?type=tutorials>`__
and `Secure
SSH <https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2>`__
tutorials for more help.

SSL test
^^^^^^^^^^^^

You can also check how secure your new web server is compared to your bank. Add this link to a web browser and wait for the results.

::

    https://www.ssllabs.com/ssltest/analyze.html?d=yourdomain.com

Now change yourdomain.com to your local bank's domain name in the link and post the results below. 
		
|

--------------------
