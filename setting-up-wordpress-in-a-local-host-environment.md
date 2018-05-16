# Setting up WordPress in a local host environment

**Tools you will need:**

1. MAMP or WAMP  - MAMP is for Mac, WAMP is for Windows. 
2. WordPress.org latest install
3. MySQL Database

 MAMP has been installed on your Macs with Bitnami. If you'd like to learn how to install WordPress with Bitnami, you can go to the following link: [https://www.howtoforge.com/installing-wordpress-with-bitnami](https://www.howtoforge.com/installing-wordpress-with-bitnami)

To start the MAMP Apache and MySQL servers, simply click "Start Servers" from the main MAMP screen. Your MAMP servers have now been started.

Once the MAMP servers start, the MAMP start page should open in your default web browser. If not, click on "Open start page" in the MAMP window. Once that's open, select phpMyAdmin from the webpage.

Under "Create new database", enter in a database name such as "wordpress", and press "Create." No need to choose an option for "collation", it will automatically be assigned by MySQL when the database tables are created, during the WordPress installation.

### WordPress Install

Now it's time to download WordPress. Navigate to WordPress.org, on the top right hand corner of the website you will see a download button. 

Once you've downloaded and unzipped the WordPress download, open up the "wordpress" folder. 

Click and drag all of the files from the wordpress folder to your MAMP document root \(/Applications/MAMP/htdocs\).

Lastly, we've got to run WordPress' famous 5-minute installation. 

Visit your local site \(localhost:port or localhost:port/wordpress\), and enter the following information into the database setup form:

```text
Database Name: wordpress
User Name (database): root
Password (database): root
Database Host/server: localhost
Table Prefix: wp_
```

Once that's complete, enter your Site Name, email address, username and password and you're good to go!

