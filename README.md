# LempBible
> This is the installation manual for the classmates that do not know how to install LEMP
## Requirements
- [ubuntu.zip in gdrive](https://drive.google.com/file/d/1c7jfkd2rhUn_EikNrxqe5uMeloL8pZzX/view?usp=drive_link)
- Internet (Of Course!)
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
```nginx
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

## TESTING PHP SOLELY
1. > Add a php test file (Its okay if its red) (Change ADD_YOUR_WEBSITE_HERE)
```bash
nano /var/www/ADD_YOUR_WEBSITE_HERE/info.php
```
2. > Add this inside the php
```php
<?php
phpinfo();
```
3. > To exit do CTRL + X then Press Y then Press Enter
4. > Test the php by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app/info.php" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)
## Testing PHP and MySQL
1. > Go to mysql
```bash
sudo mysql
```
2. > Do this thing I know you guys do not know what it does
```sql
CREATE DATABASE example_database;
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON example_database.* TO 'example_user'@'%';
```
3. > Exit MySQL
```sql
exit
```
4. > Edit the created database (password is password)
```bash
mysql -u example_user -p
```
5. > Just copy paste this... Are you looking for any description just copy this
```sql
CREATE TABLE example_database.todo_list (
    item_id INT AUTO_INCREMENT,
    content VARCHAR(255),
    PRIMARY KEY(item_id)
);

INSERT INTO example_database.todo_list (content) VALUES ("My first item");
INSERT INTO example_database.todo_list (content) VALUES ("My second item");
INSERT INTO example_database.todo_list (content) VALUES ("My third item");

SELECT * FROM example_database.todo_list;
```
6. > Exit MySQL
```sql
exit
```
7. > Add a list test file (Its okay if its red) (Change ADD_YOUR_WEBSITE_HERE)
```bash
nano /var/www/ADD_YOUR_WEBSITE_HERE/list.php
```
8. > Add this inside the php
```php
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>"; 
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```
9. > To exit do CTRL + X then Press Y then Press Enter
10. > Test the php by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app/list.php" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)
## Wordpress Installation (Finally!!!)
1. > Go here
```bash
cd /tmp
```
2. > Get the wordpress tar file
```bash
curl -O https://wordpress.org/latest.tar.gz
```
3. > Untar the file
```bash
tar -xvzf latest.tar.gz
```
4. > Move the untar file to the correct folder (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo mv wordpress /var/www/ADD_YOUR_WEBSITE_HERE/
```
5. > Change the ownership of wordpress (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo chown -R www-data:www-data /var/www/ADD_YOUR_WEBSITE_HERE/wordpress
```
6. > Change the mod of wordpress (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo find /var/www/ADD_YOUR_WEBSITE_HERE/wordpress -type d -exec chmod 755 {} \;
```
7. > Change the mod of wordpress (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo find /var/www/ADD_YOUR_WEBSITE_HERE/wordpress -type f -exec chmod 644 {} \;
```
8. > Go to wordpress (Change ADD_YOUR_WEBSITE_HERE)
```bash
cd /var/www/ADD_YOUR_WEBSITE_HERE/wordpress
```
9. > Use the sample php
```bash
sudo cp wp-config-sample.php wp-config.php
```
10. > Edit the config
```bash
sudo nano wp-config.php
```
11.  > Find this kind of syntax and change it to this (DO NOT JUST COPY PASTE)
```php
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'wpuser' );
define( 'DB_PASSWORD', 'password' );
```
12. > To exit do CTRL + X then Press Y then Press Enter
13. > Go to home
```bash
cd ~
```
14. > Add and edit the wordpress for nginx (Change ADD_YOUR_WEBSITE_HERE)
```nginx
server {
    listen 80;
    server_name your_domain;
    root /var/www/your_domain/wordpress;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
15. > To exit do CTRL + X then Press Y then Press Enter
16. > You should find the files inside  /etc/nginx/sites-enabled/ first
```bash
sudo ls /etc/nginx/sites-enabled/ 
```
17. > Whatever listed must be deleted like (Change NAME OF FILE)
```bash
sudo rm /etc/nginx/sites-enabled/<NAME OF FILE> 
```
18. > Link Nginx available to enabled
```bash
sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
```
19. > Check for errors (It must have OK and Successful at each line)
```bash
sudo nginx -t
```
20. > If there is error its either Step 4-18 is wrong and must be fix before going to the next step
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
4. >  Redo steps 18-20
***
1. >  It can be in the config file (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo nano /etc/nginx/sites-available/ADD_YOUR_WEBSITE_HERE/wordpress
```
2. >  Check the code from the step 14, changed if there is something wrong
3. >  To exit do CTRL + X then Press Y then Press Enter
4. >  Skip to step 19-20
***
1. > It could be step 11 wrong
2. > Do step 8, 10-12
3. > check wordpress again
***
1. Maybe just repeat step 5-7
### For No Errors
21. > Reload nginx
```bash
sudo systemctl reload nginx
```
22. > Do this since sometimes step 21 needs but still do it if does not
```bash
sudo systemctl daemon-reload
```
23. > (If you are at the login then go back to the terminal after going to the website to complete the installation) Visit the wordpress by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)
24. > If there is errors then go to the For errors of wordpress installation
## Fix Wordpress no CSS
1. > Open the wordpress mysql (password of mysql is password) 
```bash
sudo mysql -u root -p
```
2. > Use the wordpress table
```sql
use wordpress
```
3. > Baguhin ito (Change ADD_YOUR_WEBSITE_HERE)
```sql 
UPDATE wp_options SET option_value = 'https://ADD_YOUR_WEBSITE_HERE' WHERE option_name = 'siteurl' OR option_name = 'home';
```
4. > Exit MySQL
```sql
exit
```
5. > Last change/edit (Change ADD_YOUR_WEBSITE_HERE)
```bash
sudo nano /var/www/ADD_YOUR_WEBSITE_HERE/wordpress/wp-config.php
```
6. > Find this comment /* That's all, stop editing! */ and paste the code below above the comment
```php
define('FORCE_SSL_ADMIN', true);

if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
    $_SERVER['HTTPS'] = 'on';
}
```
7. > To exit do CTRL + X then Press Y then Press Enter
8. > Use wordpress by visiting the link Ex. "https://apple-helping-raven.ngrok-free.app/wp-login.php" in any browser even your phone (ayos lang ne meron pop up something sa link, click lang ang visit website)
   
## Common Questions
1. > How to open the server so I can use wordpress?
>> - Use ./host.sh at the start of the terminal
2. > How to close the server if not needed?
>> - Do the CTRL + C in the server ui
3. > Can I still access the wordpress even if the server is close?
>> - No you can not, only when the server is open
4. > Where to access the wordpress dashboard?
>> - Use your website name/link then add wp-login.php at the end of the file then login Ex.: https://apple-helping-raven.ngrok-free.app/wp-login.php
5. > Where to add or change the page?
>> - Go to the dashboard then top left click the menu on the right or go to the posts tab then either edit an existing post or add a new post
6. > How to edit?
>> - Click exiting text/elements at the center to edit the text/element, on the right is the selected element styles or design options and the top left thereis a plus sign to add more elements
7. > How to save and share the access of the page?
>> - Publish or Save on the top right of the editor then go back to the editor or click X after publishing then press share button at the top right and copy the link
8. > Is the access of the website unlimited?
>> - Actually NO!, It has a limit of 20000 https requests and you can check it at the ngrok website dashboard and in the left column there is a tab named Usage at the bottom
