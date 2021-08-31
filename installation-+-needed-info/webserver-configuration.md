# Webserver Configuration

{% page-ref page="installation.md" %}

{% hint style="info" %}
You must follow the Installation Instructions above!
{% endhint %}

### With SSL

{% hint style="danger" %}
TO GENERATE AN SSL YOU MUST UNPROXY PROTECTION ON CLOUDFLARE \(if you use cloudflare\). **AFTER** the SSL is generated, you can then proxy connections again.
{% endhint %}

#### SSL Creation

```text
systemctl start nginx
certbot certonly --nginx -d your.domain.com
```

If successful, you should recieve this message below!

```text
IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/your.domain.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/your.domain.com/privkey.pem
   Your cert will expire on date. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

#### Configuration

You must go to the NGINX sites directory, /etc/nginx/conf.d/  
Then you must create a new file called, your.domain.com.conf and open it  


```text
cd /etc/nginx/conf.d
touch yourdomain.com.conf
nano yourdomain.com.conf

# Make sure you press CTRL + S to save (just tryna be careful).
```

{% hint style="warning" %}
If you do NOT have Astu Panel hosted on the same machine, you **MUST** change localhost to the domain that the AstuPanel is hosted on.
{% endhint %}

```text
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}
server {
    listen 443 ssl http2;
location /afkwspath {
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  proxy_pass "http://localhost:<port>/afkwspath";
}
    
    server_name <domain>;
ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
  }
}
```

{% hint style="info" %}
Remember to change &lt;domain&gt; to your domain, and &lt;port&gt; do the port that AstuPanel is hosted on.
{% endhint %}

You can now reload nginx to finish!

```text
systemctl restart nginx
```

### Without SSL

#### Configuration

{% hint style="warning" %}
If you don't have AstuPanel hosted on the same machine, you must change localhost to the domain where the panel is hosted.
{% endhint %}

```text
server {
  listen 80;
  listen [::]:80;
  
  location /afkwspath {
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  proxy_pass "http://localhost:port/afkwspath";
}

  server_name <domain>;

  location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
  }
}
```

{% hint style="info" %}
Remember to change &lt;domain&gt; to your domain and &lt;port&gt; to the port that AstuPanel is hosted on.
{% endhint %}

