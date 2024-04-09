Today we will be set up a firewal using ufw and do backend 
# Step one
lets start of by downloading ufw on our system
run this command
```bash
sudo pacman -S ufw
```
# step two 
Now that we have ufw downloaded we can enable it
using the command below
```bash
sudo systemctl enable --now ufw.service
```
now the service is enabled but not yet started
# step three 
check the status of you ufw by running the command below
```bash
sudo ufw status verbose
```
you should get by inactive if this is your first time working with ufw
# step four
now you can add any restriction you would like to your ufw firewall
for example if you wanted to allow shh you can use ether
```bash
sudo ufw allow SSH
# or
sudo ufw allow 22
```
to limit your shh so that it will deny incoming adresses if they attempt 6 initiations in 30 seconds
you use this command 
```bash
sudo ufw limit ssh
```
and so forth there are many comgiurations you can set, a list of them is available in the ufw documentation 
# step 4
Now we have defined some rules for our firewall but have not started it 
start it using the command below
```bash
sudo ufw enable
```
# step 5 
check the status again 
using 
```bash
sudo ufw verbose
```
now you should see all the rules you have set 
# step 6
if you allow a service you didnt mean to you can delete it with 
```bash
sudo ufw delete allow SSH
```
you can also make the list a numbered one so that you can delete by number
so run 
```bash 
sudo ufw status numbered
```
this will give you the status list in numbered format
now you can pick a number and delete it usig 
```bash 
sudo ufw delete 2
```
for example
# Step 7
# Step 7
Now lets set up reverse proxy on a nginx server
first go to your nginx server file should be located in /etc/nginx/sites-available if prior steps were followed correctly
so run the command
```bash
cd /etc/nginx/sites-available
```
vim into the nginx-2420
```bash
sudo vim nginx-2420
```
# step 8
Once you are in this file you need to add a reverse proxy in the second location block
should look like this 
```
    location /api {
        # Define the reverse proxy settings
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    location /hey {
        proxy_pass http://127.0.0.1:8080/hey;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
                                                                             location /echo {
        proxy_pass http://127.0.0.1:8080/echo;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
http://127.0.0.1:8080; change this to the port you are using
# step 8
download the server backend file
from the attachments folder in the gitlab
# step 9
Now that you have the server file in your downloads you can send it to the vm usiing sptp
run 
```
sftp  -i .ssh/do-key dosan@24.199.126.94
```
then run 
```
put hello-server
```
now the server file should be in ur vm
# Step 10
Now move the servive file into ur bin directory using
```bash
mv hello-server /$HOME/bin
```
# Step 11
go into the systemd directory 
```bash
cd /etc/systemd/system
```
once here you want to create a service file
```bash
sudo vim helo-server.service
```
you can name this file anything you want but make sure it is .service
# step 12
Now place the following in this file
```
[Unit]
Description=Backend Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/hello-server
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
# step 13
now make ur hello-server executable 
# step 14
Now that we have the service file set up you can start the service
```bash
sudo systemctl start hello-service.service
```
then 
```bash
sudo systemctl enable hello-service.service
```
then to see the status and if it is running
```bash
systemctl status hello-server.service
```





