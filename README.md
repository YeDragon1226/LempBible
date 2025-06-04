# LempBible
> This is the instalation manual for the classmates that do not know how to install LEMP
## Requirements
[ubuntu.zip in gdrive](https://drive.google.com/file/d/1c7jfkd2rhUn_EikNrxqe5uMeloL8pZzX/view?usp=drive_link)
## Oracle Virtual Box Setup
1. > Open the **ubuntu.zip**
2. > Move it to any folder you picked
4. > Go to the location of Oracle Virtual Box
```bash
  C:Programs Files/Oracle/Virtual Box/
```
5. > Shift + Delete
6. > Confirm until deletion
7. > Open the **Virual Box Installer** in the folder where you move the files from the **ubuntu.zip**
8. > Next/Agree until **Finish**
9. > Repeat step 4-7
10. > Next then **Press Repair** and complete the installer until **Finish**
11. > Repeat step 7-8
## Setup Ubuntu
1. > Open the **Oracle Virtual Box**
2. > Open the **File Tab** at the top left
3. > Open the **Import Appliance**
4. > In **File** click the folder
5. > **Warning: Do not click Finish Until I Say So**
6. > Find the **ubuntu.ova** in the same location of **Virtual Box Installer**
7. > Click the **Settings**
8. > Change the Mac Address Policy to **Generate...**
9. > Click Finish
10. > Wait
11. > **Start Ubuntu**
## Setup Installation
> P.S. The password of ubuntu and the terminal is **"ubuntu"**
***
> P.S. When a pop up of update ubuntu shows just click **"Restart Later"**
***
> P.S. To copy in the terminal "Ctrl + Shift + C"
***
> P.S. To paste in the terminal "Ctrl + Shift + V" (Only copy in the Virtual Box, outside or windows copy will not work) 
***
1. > Press **Window Key** then search **Terminal** then press **Enter**
2. > To update and upgrade the packages
```bash
sudo apt update -y && sudo apt upgrade -y
```
## NGINX Installation
1. > Do the bash to install nginx and make it compatible with the network
```bash
sudo apt install nginx -y
sudo ufw app list
sudo ufw allow 'Nginx HTTP'
sudo ufw enable 
```
2. > Must see the **"IPV4 or IPV6"** if the bash done above is correct
```bash
sudo ufw status
```
## NGROK Installation (To make wordpress accessible in the internet)
1. > Setup Account in [NGROK WEBSITE](http://ngrok.com)
2. > You can skip the security authentication
3. > Go back to the terminal and do this to install the ngrok
```bash
sudo apt install curl -y
```
4. > Go back to ngrok website dashboard
5. > Find the Step 1 "Connect" in the Getting Started - Setup & Installation
6. > Find the "Installation" and copy everything into the terminal except in the "Deploy your app online"
7. > Lets add a script to ease making server online and first make a script file
```bash
touch host.sh
```
8. > Open the file
```bash
nano host.sh
```
9. > Add this to the file and the code below at "Below Here" is from the "NGROK website" "Deploy your app online (Static Domain and not the Ephemerial Domain)", click the "Claim free static domain" then copy it below the "Below Here"
```bash
#!/bin/bash
#Below Here
```
10. > CTRL + X then press Y then press Enter to exit nano
11. > To make host.sh run, do this
```bash
sudo chmod +x host.sh
```
12. > To run the server just do
```bash
./host.sh
```
or
```bash
bash host.sh
```
13. > You can test the ngrok by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)
14. > To keep ngrok running in terminal, in the terminal there is a top left button, click it. This will make a new tab
15. > You can now switch between tabs at the top from server to additinal terminal
### Notes 
> To close the server/ngrok just CTRL + C
***
> To run it again just do
```bash
./host.sh
```
or
```bash
bash host.sh
```
## MYSQL Installation
1. > Do this to install mysql
```bash
sudo apt install mysql-server -y
```
2. > Do this to do mysql setup
```bash
sudo mysql_secure_installation
```
3. > Do this in order, Pres Y then Press 0 then Press Y then Press Y then Press N then Press Y
4. > Do this to test mysql (no password for mysql so sudo is used)
```bash
sudo mysql
```
5. > Just do this to exit mysql
```bash
exit
```
## PHP Installation
1. > Do this to install php
```bash
sudo apt install php-fpm php-mysql php-curl php-mbstring php-imagick php-xml php-zip
```
## Connecting PHP and Testing Nginx
P.S All code forward will mostly contain ADD_YOUR_WEBSITE_HERE it must be changed to your website name EX. apple-serving-pegion.ngrok-free.app
1. > Do this to make a new folder for your website (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo mkdir /var/www/ADD_YOUR_WEBSITE_HERE 
```
2. > To make the folder usable (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo chown -R $USER:$USER /var/www/ADD_YOUR_WEBSITE_HERE 
```
3. > To edit nginx (its okay if its red) (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo nano /etc/nginx/sites-available/ADD_YOUR_WEBSITE_HERE
```
4. > Add this inside the file (Change ADD_YOUR_WEBSITE_HERE)
```
server {
    listen 80;
    server_name ADD_YOUR_WEBSITE_HERE;
    root /var/www/ADD_YOUR_WEBSITE_HERE;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
5. > To exit do CTRL + X then Press Y then Press Enter
6. > Link Nginx available to enabled (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo ln -s /etc/nginx/sites-available/ADD_YOUR_WEBSITE_HERE /etc/nginx/sites-enabled/
```
7. > Remove this since it may result to error if not
```bash
sudo unlink /etc/nginx/sites-enabled/default
```
8. > Check for errors (It must have OK and Successful at each line)
```bash
sudo nginx -t
```
9. > If there is error its either Step 4-6 is wrong and must be fix before going to the next step
### For Errors
1. > If there is error with somehing like /etc/nginx/sites-enabled/ADD_YOUR_WEBSITE_HERE
2. >  You should find the files inside  /etc/nginx/sites-enabled/ first
```bash
sudo ls /etc/nginx/sites-enabled/ 
```
3. >  Whatever listed must be deleted like (Change NAME OF FILE)
```bash
sudo rm /etc/nginx/sites-enabled/<NAME OF FILE> 
```
4. >  Redo step 6 and 8-9
***
1. >  It can be in the config file (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo nano /etc/nginx/sites-available/ADD_YOUR_WEBSITE_HERE
```
2. >  Check the code from the step 4, changed if there is something wrong
3. >  To exit do CTRL + X then Press Y then Press Enter
4. >  Skip to step 8 and 9
### For No Errors
10. > Reload nginx
```bash
sudo systemctl reload nginx
```
11. > Add and edit (its okay if its red)
```html
<html>
  <head>
    <title>Testing</title>
  </head>
  <body>
    <h1>Hello World!</h1>

    <p>This is the landing page for<strong>Testing</strong>.</p>
  </body>
</html>
```
12. >  To exit do CTRL + X then Press Y then Press Enter
13. > Test the ngrok by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)


