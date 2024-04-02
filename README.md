The goal of these instructions is to teach you how to deliver static html through a nginx server

# 1)The first step is too upgrade you packages. You can do this by using the command 
''''bash
sudo pacman -Syu 
''''
# 2)The second step is to download vim 
by using the command 
''''bash
sudo pacman -S vim
''''
# 3) the third step is to download nginx through the command below
''''bash
sudo pacman -S nginx
''''
# 4)the fourth step is to download git on your vm using
''''bash
sudo pacman -S git
''''
Now that we have everything downloaded we can start and enable nginx

# 5) start nginx using the command below
''''bash
sudo systemctl start-nginx
''''
Now we need to enable nginx so that it starts at boot

# 6) Enable nginx using
''''bash
sudo systemctl enable-nginx
''''
# 7) Now create a project root 
''''bash
sudo mkdir -p /web/html/nginx-2420
''''
the -p makes our life easier by creating any needed parent directories for us

Now we need to create two directories that will contain our server blocks and help us create a symlink

# 8) To create the directories run the below commands
''''bash
sudo mkdir /etc/nginx/sites-available
sudo mkdir /etc/nginx/sites-enabled
''''
Now we neeed to create a file inside the site-available directory that will contain our server blocks 
# 9) to create the file use 
''''
cd /etc/nginx/sites-available

vim nginx-2420.conf
''''
using vim to create the file sould automatically take you to the vim interface.

# 10) add server blocks to the vim file you are in
''''
server {
    listen 80;
    listen [::]:80;
    server_name domainname1.tld;
    root /usr/share/nginx/domainname1.tld/html;
    location / {
        index index.php index.html index.htm;
    }
}
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    http2 on;

    ...
}
''''
Now add the site-enabled to the end of the nginx.conf file

# 11) go into the /etc/nginx directory
then get into the conf file using vim
''''
sudo vim nginx.conf
''''
add this to the bottom of the file
''''
8 http {
119
120         include sites-enabled}
''''

# 12) Now restart your nginx
''''
sudo systemctl restart nginx.service
''''

# 13) create a html file in the project directory we made at the begining
''''
cd /web/html/nginx-2420

touch example.html
''''
now copy the html code that is givin in the html file.

Done






