#self-taught 
On Debian/Ubuntu:
```bash
sudo apt install fail2ban

# jail.local gets read after jail.conf, it is better to create it instead of modifying directly jail.conf
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo vim /etc/fail2ban/jail.local
```

```jail.local
[sshd]

enabled = true
port    = ssh
backend = systemd
maxretry = 2
findtime = 3600 # for 1 hour
bantime = 86400 # for 1 day
ignoreip = 127.0.0.1
```

```shell
sudo systemctl restart fail2ban
```
# Monitoring
```shell
sudo fail2ban-client status sshd
sudo iptables -L -n
```
# Unbanning
```shell
sudo fail2ban-client unban --all

sudo fail2ban-client unban <ip-address>
```