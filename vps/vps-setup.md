# VPS Setup Guide

## Connect
```bash
ssh root@ip
```

## Update
```bash
apt update && apt upgrade -y
```

## Timezone
```bash
timedatectl set-timezone Europe/Kyiv
```

## New user
```bash
adduser newuser
usermod -aG sudo newuser
```

## SSH Keys
### Local Machine
```bash
ssh-keygen -t ed25519 -C "user@vps"
cat ~/.ssh/id_ed25519.pub
```
### VPS
```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys # Insert the key
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## SSH Config
```bash
sudo nano /etc/ssh/sshd_config
```
```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
Port 2233 # or another
MaxAuthTries 3
AllowUsers newuser
PermitEmptyPasswords no
```
Leave the old SSH session open while you test the new port

## Firewall (UFW)
```bash
sudo ufw allow 2233
sudo ufw enable
sudo ufw status # Be sure to check the open port
sudo ufw reload
sudo systemctl restart ssh
```

## Fail2ban
```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
sudo fail2ban-client status
```

## Htop
```bash
sudo apt install htop -y
htop
```

## Security updates automatically
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```