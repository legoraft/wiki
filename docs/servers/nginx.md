# Nginx

Nginx (pronounced engine-x) is a web server and reverse proxy, which I use to proxy my servers from my homelab.

## Installation

To set up nginx, you first need to install the `nginx` package. This package is probably just named nginx on most distros, but check it for yourself.

To install Nginx on Debian, just use the following command:

```bash
sudo apt install nginx
```

On installing the package, a systemd service is started with nginx, so you can go on to configuring your reverse proxy.

## Configuration

To configure a reverse proxy with nginx, you need to add a file to the `conf.d` directory. This can be done as follows:

```bash
sudo nano /etc/nginx/conf.d/example.conf
```

> **Note:** In some tutorials the `sites-available` directory is used, this isn't a directory that is available on all distros, so use `conf.d` for distro-agnostic installations.

You can name this file whatever you want, I mostly name them after the services they proxy.

To configure your proxy you have to enter some lines to your file:

```nginx
server {
	listen 80;
	listen [::]:80;
	server_name subdomain.domain.tld

	location / {
		proxy_pass https://192.168.x.x:0000

		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
		proxy_set_header Host $host;

		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-Port $server_port;
	}
}
```

Within this configuration, you have to adjust some parameters. First, you need to adjust your `server_name` to whatever domain or subdomain you have or want. You also need to adjust the `proxy_pass` to the local ip and port of the server you want to proxy.

You can keep the other things the same, this needs to be added to every proxy.

After configuring the reverse proxy, you can check the config and restarting nginx by running

```bash
sudo nginx -t
sudo systemctl restart nginx
```

After restarting, you'd probably want to add an ssl certificate to use https on your proxy. This can be done easily and free with let's encrypt. Before you do that, however, you'd want to add an A record to your domain name.

## Domain name

To add a record to your domain name, go to your domain name provider and add an A record in the dns settings. This A record should point to your public IP and have the same domain name as you configured. 

You probably should also add an SRV record to point to the correct port, which can be somewhat different for different providers, so reference their documentation on that.

## SSL certificate

To install let's encrypt on Debian, you can just use the following commands (check the package name for your distro):

```bash
sudo apt install certbot python-certbot-nginx
```

To acquire the certificate for the domain name you just chose for the reverse proxy you just need to run the following command:

```bash
sudo certbot --nginx -d subdomain.domain.tld
```

When running this you need to enter some information, after which your certificate will be set up.

## Set up cronjob

Certbot certificates expire every 90 days, so I always set up a cronjob to refresh my certificates. This is quite easy to do, just open the crontab file by entering:

```bash
crontab -e
```

Within the file enter the following line:

```cron
0 24 * * * /usr/bin/certbot renew --quiet
```

This line runs the command every 24 hours, and causes no extra output thanks to the `--quiet` flag.