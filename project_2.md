### In this project I will be implmenting web solutions deployment using LA(E)MP stacks. This stack uses the **NGNIX** web server ##.
<br>

### 1. Installing the *Ngnix* web server
### The ***Ngnix*** is a high performance web server used to display web pages to site visitors. 
<br>

- Update the server's package index and use the ***apt*** package manager to install ***nginx*** 

![update](./images/update.PNG)

![update](./images/ngnix.PNG)

- Check the status of your web server installation

    *sudo systemctl status nginx*

    If you already have apache server running on your machine, you will get an error message when you try to check nginx status. It means you already have a process bound to **HTTP port 80** (because after you upgraded the system, it will start apache2 by default). To solve this problem, first stop the apache2 service <br>

    *sudo service apache2 stop* 
    <br>
[click here for more](https://stackoverflow.com/questions/51525710/nginx-failed-to-start-a-high-performance-web-server-and-a-reverse-proxy-server) <br> If  everything is good you should get something that looks like the image below <br>
![update](./images/ngnix_fixed.PNG) <br>
move to the last line and hit *q* botton on the keyboard to exit or *:* then *q* 




    ### This was very helpful:
    ### I mistakenly killed a process running on a port on my linux server, this link helped me resumed it 
    [click here](https://ostechnix.com/suspend-process-resume-later-linux/)

    [for some more details click here](https://www.ibm.com/docs/en/aix/7.1?topic=processes-restarting-stopped-process)
<br>

    I had to re-create another EC2 instance to install *nginx* web server, beacuse I had some challenges on getting it to work properly on the server which had apache2 pre-installed.

    Nginx works well now
    ![update](./images/nginx_working.PNG)

### 2. Installing ***MYSQL***
- Install *mysql* from apt manager
<br>

    ![update](./images/mysql_install.PNG)

<br>

- Launch *mysql* 
<br>

    ![update](./images/mysql_launch.PNG)
<br>
If you want more information about setting the password to *mysql* server, [click here](https://exerror.com/failed-error-set-password-has-no-significance-for-user-rootlocalhost-as-the-authentication-method-used-doesnt-store-authentication-data-in-the-mysql-server/)

- here you run ***ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'mynewpassword';*** on *mysql* environment (***sudo mysql*** takes you there, after installation) 
<br>

![update](./images/mysql_passwd.PNG)

- Exit *mysql* window and run ***sudo mysql_secure_installation*** you'll be required to type the password you specified above (***mynewpassword***), then required to chabge it.

    <br>![update](./images/password_1.PNG)


- Proceed to make the following change
![update](./images/password_2.PNG)
Then ***exit*** *mysql*

- Load *mysql* with the *p* tag i.e ***sudo mysql -p*** <br>
then input your password
<br>

    ![update](./images/mysql_load.PNG)

<br>

### 3. Install *PHP* for *NGINX* server
You will need to install "PHP fastCGI process manager" (***php-fpm***) which is an external program that handles *PHP* processing and acts as a bridge between *PHP* interpreter itself and the *Nginx* web server. While *Apahe* embeds the *PHP* interpreter in each request, the *Nginx* requires this external program. 

<br>

![update](./images/install_php.PNG)

<br>

### 4. Configure *NGINX* to use *PHP* processor
- Create a new domain <br>
Just as with the Apache server, we can create server blocks (virtual hosts) to encapsulate configuration details and host more than one domain on a single Nginx server. By default Nginx has one server block enabled and configured to serve documents out of a directory */var/www/html* This works well for a single site and becomes difficult to manage if we are hosting multiple sites. Here we create a new domain, ***projectLEMP*** (i.e. a root web directory and assign ownership).<br>

    ![update](./images/rootweb.PNG)

- Configuration file <br>
    Create a configuration file in Nginx's sites-available directory (make sure you create the file using superuser permission, *sudo*, else you won't be allowed to save it) and add the bare-bones configuration settings. [click here](https://www.darey.io/docs/step-4-configuring-nginx-to-use-php-processor/) <br>

    Then activate your configuration by linking to the config file from Nginx's *sites-enabled* directory. This will tell Nginx to use the configuration next time it is loaded. Test your configuration for syntax errors 
    <br>

    ![Config](./images/nginx_config.PNG)
    
    Disable the default *Nginx* host that is corrently configured to listen on port 80, by unlinking it.

    Then reload *Nginx* to apply the changes. <br>

    ![Config](./images/reload.PNG)

    Create an ***index.html*** file in the recently created root web location (*/var/www/projectLEMP*) to test that the virtual host works (paste your public IP address in a browser).<br>

    To find out your public IP address: <br>
    ***curl -s http://169.254.169.254/latest/meta-data/public-ipv4***
    <br>
    To find out your public hostname (DNS name): <br>
    ***curl -s http://169.254.169.254/latest/meta-data/public-hostname*** <br>

    ![Config](./images/ip.PNG)

    Now, the LEMP stack is fully configured. Next is to create a *PHP* script to test that *Nginx* is able to handle *.php* files within the newly configured website.

    For now, we will leave the newly created *.html* file as temporary landng page for our application until we setup *.php* file to replace it. When you do this, always remember to remove or rename the *index.html* file from your document root as it would take precedence over an *index.php* file by default (although, you can change this hierarchy from your configured file in  ***/etc/nginx/sites-available/projectLEMP***). 
    
    <br>


### 5. Testing *PHP* with *NGINX*
-   Here we want to test that *Nginx* can corretly hand *.php* files off to your *PHP* processor. and we do this by creating a test *php* file in the document root 










     
    












 




