# [WordPress Free ForEver](https://youtube.com/playlist?list=PLETG2T1KvnipE7yQx5YJ5voZYUuG3WZQn "I curated a playlist of the episodes that taught me how to set up my blog on Google Cloud Platform free forever, .com URLs are $1 a month.There are several other options, but the free server generally doesn't have enough RAM for what you're asking it to do, so what he does with the SWAP file is a great idea.You may need to brush up on your Vim Commands to edit that part and adding the Encryption Certificates is another huge advantage!Revere Poxy with NGINX and DockerFiles! feel free to send me a message if you get stuck anywhere")
## **#2 SwapFile**

```bash
sudo apt update
apt list --upgradeable
sudo apt upgrade
sudo apt update
top
# sudo fallocate -l 4G /swapfile
sudo fallocate -l 8G /swapfile
cd /
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
top
sudo apt install -y nano
sudo nano /etc/fstab
```

### **7:18**

```bash 7:18
/swapfile none swap sw 0 0
```

```bash
sudo reboot
top
curl https://get.docker.com > install-docker.sh
# chmod 755 install-docker.sh
chmod 100 install-docker.sh
sudo ./install-docker.sh
sudo usermod -aG docker dev_turtlewolfe
sudo docker container ls
sudo reboot
docker container ls
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
sudo apt install -y git
```

make sure you're back in home ~

<!-- git clone https://github.com/chrisbmatthews/wordpress-docker-compose.git -->

```bash
git clone https://github.com/TurtleWolf/wordpressMathews
cd wordpressMathews/
```

### **11:45 also edit passwords at this point**

```bash
nano .env
    IP=127.0.0.1
    DB_ROOT_PASSWORD=alphaa
    DB_NAME=charlie
chmod 400 .env
chmod 400 docker-compose.yml
# BACKUP server SNAPSHOT
docker-compose up -d
docker container ls
```

## **#3 Point DNS @ Cloud IP**

1. static IP
1. DNS @ A & www CNames 3:13

```bash
dig scripthammer.com
```

## **#4 NGINX Reverse Proxy**

### **:50** setting, general 2 URLs

### **3:55**

```bash
docker container ls
nano docker-compose.yml
docker-compose down
docker ps
docker ps -a
docker-compose up -d
docker ps
```

### **7:15** defaults to port 80

```bash
sudo apt install -y nginx
cd /etc/nginx
cd sites-available/
nano default
sudo nano www.ScriptHammer.com.conf
```

```conf
server {
    root /var/www/html;
    listen 80;
    listen [::]:80;
    server_name scripthammer.com www.scripthammer.com;
    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Host $server_name;
        proxy_set_header X-Forwarded-Proto \$scheme;
        }
    }
```

### (#4 10:54)

```bash
cd ..
cd sites-enabled/
sudo ln -s /etc/nginx/sites-available/www.ScriptHammer.com.conf www.ScriptHammer.com.conf
cat www.ScriptHammer.com.conf
sudo service nginx restart

sudo apt autoremove
```

## **#5 HTTPS Let's Encrypt**

### **3:00**

```bash
sudo apt install software-properties-common && sudo apt update
```

<!-- sudo apt update   -->
<!-- apt list --upgradeable   -->
<!-- sudo apt upgrade   -->

```bash
sudo add-apt-repository ppa:certbot/certbot
sudo apt update
sudo apt install -y python-certbot-nginx
sudo apt install -y python3-certbot-nginx
```

<!-- choose location   -->

```bash
# cd ..
# cd sites-available/
cd /etc/nginx/sites-available
sudo certbot --nginx -d scripthammer.com -d www.scripthammer.com
```

<!-- sudo certbot --nginx -d scripthammer.com -->
<!-- redirect unsecure   -->

```bash
cat www.ScriptHammer.com.conf
sudo service nginx restart
```

### **8:40**

```bash
cd wordpress-docker-compose/
cd wp-app/
sudo vi wp-config.php
```

```php
if ($_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https')
    $\_SERVER['HTTPS']='on';

if (isset($_SERVER['HTTP_X_FORWARDED_HOST'])) {
    $\_SERVER['HTTP_HOST'] = \$\_SERVER['HTTP_X_FORWARDED_HOST'];
}
```

```php
define('FS_METHOD','direct');
```

```bash
cd ..
docker-compose stop
docker-compose start
```

### **11:21** wp-admin/options-general.php

1. https
1. https

### **11:40**

```bash
docker-compose stop && docker-compose start
sudo certbot renew
cd /etc
cd /letsencrypt
cd letsencrypt/
sudo crontab -e
```

### **13:12**

```bash
45 2 * * * certbot renew > /tmp/certbotrenew.log
```

```bash
    1  history
    2  docker ps
    3  docker-compose up -d
    4  ll
    5  cd wordpressMathews/
    6  history
    7  docker-compose up -d
    8  docker container ls
    9  docker ps
   10  docker container ls
   11  clear
   12  cd /etc/nginx
   13  ll
   14  cd sites-available
   15  ll
   16  nano default
   17  sudo nano www.ScriptHammer.com.conf
   18  ll
   19  sudo nano www.ScriptHammer.com.conf
   20  nano default
   21  sudo nano www.ScriptHammer.com.conf
   22  cd ..
   23  cd sites-enabled
   24  ll
   25  sudo ln -s /etc/nginx/sites-available/www.ScriptHammer.com.conf www.ScriptHammer.com.conf
   26  cat www.ScriptHammer.com.conf
   27  sudo service nginx restart
   28  cd
   29  ll
   30  docker-compose down -v
   31  cd wordpressMathews/
   32  docker-compose down -v
   33  history
```

```bash
   34  sudo apt install software-properties-common && sudo apt update
   35  sudo add-apt-repository ppa:certbot/certbot
   36  sudo apt update
   37  sudo apt install -y python-certbot-nginx
   38  sudo apt install -y python3-certbot-nginx
   41  cd /etc/nginx/sites-available
   42  sudo certbot --nginx -d scripthammer.com -d www.scripthammer.com
   44  cat www.ScriptHammer.com.conf
   45  sudo service nginx restart
   49  cd /wordpressMathews
   50  docker-compose up -d
```

sudo chown -R www-data <path>/wp-content/uploads
sudo chown -R www-data ~/pohlnerlandscaping/wp-app/wp-content/uploads
