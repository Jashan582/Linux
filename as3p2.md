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






