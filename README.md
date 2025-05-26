MTProto Proxy Whitelist Installer
=================================

A robust Bash script for automated installation, configuration, and management of a secure MTProto Telegram proxy environment, complete with an NGINX reverse proxy, PHP whitelist portal, Telegram integration, enhanced security, and automation features.

Features
--------
- MTProto Proxy management (Python or Erlang based)
- NGINX reverse proxy setup with stream module and whitelist enforcement
- Secure web whitelist portal (PHP, password & token-protected)
- Automatic SSL with Certbot (or self-signed fallback)
- Fail2ban and UFW firewall integrated for enhanced security
- Telegram bot integration for whitelisting via chat
- Automated backups and permission repair
- Random fake HTML site for plausible deniability
- Automated cleanup of expired whitelist entries (cron-ready)
- Menu-driven management and Telegram user database

Quick Install
-------------
    curl -O https://raw.githubusercontent.com/jeet8200/iwasbored/main/start.sh
    sudo apt update
    sudo apt install unzip dos2unix -y
    dos2unix start.sh
    chmod +x start.sh
    sudo bash start.sh

    Note: Run as root or with sudo!

Main Menu Options
-----------------
1. Install MTProto Proxy only (choose Python or Erlang version)
2. Install Whitelist System (NGINX, PHP, firewall, Fail2ban)
3. Generate access URL with tokens (for secure IP whitelisting)
4. Fix permissions (repair file/directory permissions)
5. Change whitelist password
6. Check system status
7. Uninstall everything (full wipe)
8. Send whitelist link via Telegram
9. Random Fake HTML site (for plausible deniability)<br>
M. Manage Telegram Users (add/edit/delete user records)<br>
A. Clean Old Whitelisted IPs (remove expired entries)<br>
0. Exit

How It Works
------------
NGINX Stream Proxy
- NGINX listens on a secure port, proxies to your MTProto backend
- Only whitelisted IPs (in /etc/nginx/whitelist.txt) can connect

Web Whitelist Portal
- Access via HTTPS on your configured domain/port
- Add your IP with password + time-limited or one-time token
- Tokens generated securely; one-time tokens are tracked and cannot be reused

Telegram Integration
- Save user/chat info and proxy links
- Send whitelist links directly via Telegram bot

Security
- All credentials stored securely (root or www-data only)
- Fail2ban jail for brute-force attempts on the web portal
- Automated backups before critical changes

Automation
- Cron-ready scripts for daily whitelist and template cleanups
- Random HTML site deploys for hiding the real portal

Configuration Files & Paths
---------------------------
- Script config: /etc/mtproxy-whitelist.conf
- Whitelist: /etc/nginx/whitelist.txt
- Password: /etc/nginx/.password
- Used Tokens: /etc/nginx/used_tokens.txt
- Telegram users: /etc/nginx/telegram_users.txt
- Telegram bot token: /etc/nginx/mtproxy-whitelist.conf.telegram_token
- PHP portal: /var/www/html/post.php
- NGINX stream conf: /etc/nginx/stream.d/mtproto.conf
- NGINX site conf: /etc/nginx/sites-available/whitelist_gateway

Uninstall
---------
Choose menu option 7 for a complete uninstall, including:
- All installed packages (nginx, php, fail2ban, etc.)
- Configuration and website files
- Firewall rules

Automate Maintenance
-------------------
Whitelist cleanup:
    Add to root crontab for daily cleanup:
    0 3 * * * /bin/bash /path/to/start.sh --clean-whitelist >> /var/log/mtproxy-whitelist.log 2>&1

Random HTML refresh:
    Add to root crontab for new fake site every 6 hours:
    0 */6 * * * /bin/bash /path/to/start.sh --random-template >> /var/log/mtproxy-whitelist.log 2>&1

Troubleshooting
---------------
- Check system status from the menu (option 6)
- Its always RECOMMANDED to reboot After first Cycle of Install
- NGINX and PHP-FPM must be running
- UFW firewall should allow necessary ports
- All config and data files must be readable/writable by www-data/root
- Check logs: /var/log/mtproxy-whitelist.log and /var/log/nginx/error.log
- Change mtprotoProxy Listen Ip to 127.0.0.1 

Credits
-------
- MTProto Proxy: alexbers/python-telegram-mtproto-proxy and Erlang seriyps/mtproto-proxy
- Pick the One THat woRks for ur vps it migh be diffrent  
- Random Fake HTML: GFW4Fun/randomfakehtml

Feel free to contribute or open issues! This project is a work in progress.
