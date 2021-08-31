---
description: Installation steps!
---

# Installation

{% hint style="info" %}
The installation documentation is for Ubuntu ONLY! 
{% endhint %}

## Installing Dependencies!

```
sudo apt update && sudo apt upgrade
sudo apt install git
curl -fsSL https://deb.nodesource.com/setup_12.x | sudo bash -
apt install nodejs
npm -v
# If npm isn't a valid command, run the step below.
sudo apt install npm

```

### Nginx \(Optional Webserver, but preferred\)

```text
apt install nginx
sudo apt install certbot
sudo apt install -y python3-certbot-nginx
```

### Astu Panel Setup

```text
# With Git
git clone https://github.com/AstuHosting/AstuPanel.git
cd astupanel
npm install

# Without Git
cd (folder name)
npm install
```

