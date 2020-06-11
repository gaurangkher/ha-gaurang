= Gaurang's Home Assistant Configs =

== Setup ==
Install as python virtual env on rhel
DNS with DuckDNS
Hosted with Nginx


Nginx Configs
~~~~
server {
    listen       80 ;
    listen       [::]:80 ;
    server_name  <mydomain>.duckdns.org;
    root         /usr/share/nginx/html;

    include /etc/nginx/default.d/*.conf;

    location / {
        proxy_pass http://127.0.0.1:8123;
        proxy_set_header Host $host;
        proxy_redirect http:// https://;
        proxy_http_version 1.1;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    location /api/websocket {
	proxy_pass http://localhost:8123/api/websocket;
	proxy_set_header Host $host;
	proxy_http_version 1.1;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection "upgrade";
    }

#managed by Certbot
listen [::]:443 ssl ipv6only=on;
listen 443 ssl;
ssl_certificate </path/to/fullchain.pem>
ssl_certificate_key </path/to/privkey.pem>
include /etc/letsencrypt/options-ssl-nginx.conf;
ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}}
~~~~

== Integrations ==
* Zwave
* HACS (manual install: needed couple of try's and add some folders like www manually )
* Zeroconf integrations [LG, Samsung, Hue]
* Jupyter addon (Manual installation) - Doesnt work yet, Nginx config, reverse proxy issue
* Static Websites hosted in www

== Still in Development ==


