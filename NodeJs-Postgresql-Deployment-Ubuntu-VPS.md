
# NodeJS + Postgresql Deployment

A Step By Step Guide to deploye a NodeJS + Postgresql Application using PM2, NGINX as a reverse proxy

### 0- Generate SSH
[Click here to => How to generate it](https://docs.vultr.com/how-do-i-generate-ssh-keys?_gl=1*1teljyz*_ga*NDA3Mzk0NC4xNzE2NjIyOTAw*_ga_K6536FHN4D*MTcxNjYyODk0NS4zLjEuMTcxNjYyOTEwNy4yMC4wLjA.)


### 1- Install Node
Visit This link and follow the steps

https://github.com/nodesource/distributions


### 2- Install Git if not installed
Follow the steps on this link to install it on debian (Already installed on Ubuntu)

https://www.digitalocean.com/community/tutorials/how-to-install-git-on-debian-10

### 3- Clone your repository

### 4- Install the dependencies
- cd [Project Name]
- npm install

### 5- Setup PM2 (This makes sure that your app keeps running)
- sudo npm i pm2 -g
- Usage Guideline https://pm2.keymetrics.io/docs/usage/quick-start/

### 6- Setup UFW Firewall
- sudo ufw enable
- sudo ufw status
- sudo ufw allow ssh (Port 22)
- sudo ufw allow http (Port 80)
- sudo ufw allow https (Port 443)

### 7- Install NGINX and Configure
- cd /etc/nginx/sites-available
- nano [appname].conf
- Add the following to that [appname].conf
```
server {
        listen 80;
        server_name [Server IP];
           location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
           }
}
```
- Save it
- Then link that config file to sites-enabled running the following command
```
sudo ln -s /etc/nginx/sites-available/[appname].conf /etc/nginx/sites-enabled/
```
- Restart Nginx 
```
sudo service nginx restart
```
### 8- Install Postgresql
- [Click Here To See The Guideline](https://www.digitalocean.com/community/tutorials how-to-install-postgresql-on-ubuntu-20-04-quickstart)
### 9- Change Postgresql user default password & Create Database
- sudo -i -u postgres
- psql
- Create a Database
- createdb [Database Name]
- ALTER USER postgres PASSWORD [New Password;


