# AWS-notes
## To host a node.js site on AWS EC2 instance
* First create an EC2 instance
* clone the repository from the github into a local folder
* change directory to root
* create a configuration file by typing "sudo nano /etc/nginx/sites-available/demo"
* server{
 listen 80;
 server_name your_domain_or_ip;

 location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        }
 }
 * create symbolic link of demo in sites-enabled directory by typing
   "sudo ln -s /etc/nginx/sites-available/demo /etc/nginx/sites-enabled"
* test file sudo nginx -t
* sudo service nginx restart
* Make sure pm2 is installed in the local folder to be deployed
* If not installed type command in the site directory "npm i -g pm2"
* Then type "pm2 start npm --name "deployed nextjs demo" --start"
* pm2 ls
* Now your project is online
