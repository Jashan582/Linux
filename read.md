The goal of these instructions is to teach you how to deliver static html through a nginx server

1)The first step is too upgrade you packages. You can do this by using the command 
''''bash
sudo pacman -Syu 
''''
2)The second step is to download vim 
by using the command 
''''bash
sudo pacman -S vim
''''
3) the third step is to download nginx through the command below
''''bash
sudo pacman -S nginx
''''
4)the fourth step is to download git on your vm using
''''bash
sudo pacman -S git
''''
Now that we have everything downloaded we can start and enable nginx

5) start nginx using the command below
''''bash
sudo systemctl start-nginx
''''
Now we need to enable nginx so that it starts at boot

6) Enable nginx using
''''bash
sudo systemctl enable-nginx
''''
7) Now create a project root 
''''bash
sudo mkdir -p /web/html/nginx-2420
''''
the -p makes our life easier by creating any needed parent directories for us

Now we need to create two directories that will contain our server blocks and help us create a symlink

8) To create the files run the below commands
''''bash
sudo mkdir /etc/nginx/sites-available
sudo mkdir /etc/nginx/sites-enabled
''''

9) 
