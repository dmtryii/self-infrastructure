# Nginx Setup Guide

## Install Nginx
```bash
sudo apt update
sudo apt install nginx -y
```

## Start and enable Nginx service
```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```
## Allow Nginx through the firewall
```bash
sudo ufw allow 'Nginx Full'
sudo ufw reload
```