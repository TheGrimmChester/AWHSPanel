![AWHS Logo](https://nicolasmeloni.ovh/images/awhspanel.png)  
Automated Web Hosting Solution (AWHS) Panel

#Requirements
* For now, AWHSPanel only supports **Debian 8** but its architecture allows easy new implementations.
* (1) MySQL 5.5 & later Database
* Apache >= 2.2 OR Nginx; git; php >= 5.5;

#Installation
In this guide the installation will be in `/usr/local/awhspanel`  
1. Create the panel directory: `mkdir -p /usr/local/awhspanel/panel`  
2. Clone this repo in the directory created previously.  
`cd /usr/local/awhspanel/panel ; git clone https://github.com/TheGrimmChester/AWHSPanel.git .`  
3. Install Composer:  
`curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer`  
4. Configure the database access:  
`mv app/config/parameters.yml.dist app/config/parameters.yml`  
Edit the `app/config/parameters.yml` file with your own access.  
5. In the same file you have to change the secret string:  
You can use this website: [http://nux.net/secret](http://nux.net/secret) to help you.  
6. From the ¨panel¨ directory:  
`composer install`  
7. Uncomment few lines in `app/AppKernel.php` (l.19-20 & l.31)  
* new FOS\UserBundle\FOSUserBundle(),
* new FM\BbcodeBundle\FMBbcodeBundle(),
* $bundles[] = new Doctrine\Bundle\FixturesBundle\DoctrineFixturesBundle();  

8. Basic Apache 2.4 VirtualHost  
```text
<VirtualHost *:80>
    #ServerName www.example.com
    ServerAdmin webmaster@localhost
    DocumentRoot /usr/local/awhspanel/panel/web
    Options None

    <Directory /usr/local/awhspanel/panel/web>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```  
9. You may have to set permissions back to www-data  
`chown -R www-data:www-data /usr/local/awhspanel/panel/*`

##Ready to Use
Now the base is functional. You can install our bundles.

##Bundles
###Core Bundles
* [UserBundle](https://github.com/TheGrimmChester/UserBundle)
* [CoreBundle](https://github.com/TheGrimmChester/CoreBundle)
* [CrmBundle](https://github.com/TheGrimmChester/CrmBundle)
* [TaskBundle](https://github.com/TheGrimmChester/TaskBundle)

###Extra Bundles (not currently available)
* [WebHostingBundle](#)

##Questions and Issues
* [Join the discussion on Discord](https://discord.gg/HxNXfJK)
* [Open an issue on GitHub](https://github.com/TheGrimmChester/AWHSPanel/issues)
