# Setting Up HTTPS with Certbot on Nginx

## Install required packages
```bash
sudo apt update
sudo apt install python3 python3-dev python3-venv libaugeas-dev gcc
```

## Create a virtual environment for Certbot
```bash
sudo python3 -m venv /opt/certbot/
```

## Install Certbot and the Nginx plugin
```bash
sudo /opt/certbot/bin/pip install --upgrade pip
sudo /opt/certbot/bin/pip install certbot certbot-nginx
```
## Create a symbolic link for easy access to the certbot command
```bash
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

## Obtain and install SSL certificates for your domain
```bash
sudo certbot --nginx
```

## Set up a cron job to renew certificates
```bash
echo "0 0,12 * * * root /opt/certbot/bin/python -c 'import random; import time; time.sleep(random.random() * 3600)' && sudo certbot renew -q" | sudo tee -a /etc/crontab > /dev/null
```

## Verify the cron job has been added
```bash
sudo cat /etc/crontab | grep certbot
```