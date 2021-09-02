# Configure Your Own WAMP Server on Windows

## A. Install and Configure PHP

### A.1 Download and extract PHP

At the time of writing this guide, PHP 8.0.9 was the latest stable version available. Download preferred PHP binary zip file from https://windows.php.net. There are two types of zip files available: 

- *Thread Safe*
- *Non-thread Safe*. 

We'll use `thread safe version` for our guide.

To know more about the difference, visit [PHP configuration instructions for IIS server](https://docs.microsoft.com/en-us/iis/application-frameworks/install-and-configure-php-on-iis/install-and-configure-php).

After downloading, open the zip file and extract all your files to C:\server\php. Navigate to C:\server\php.

#### A.1.1 Rename php.ini

Search for the file, `php.ini-development` and rename it to `php.ini`.

#### A.1.2 EDIT php.ini

Open up `php.ini` using any text-editor.

There are in total two edits in this file.

- Find `extension_dir = "./"` and replace it with `extension_dir = "C:/server/php/ext"` and remember to remove semicolon(;) at its starting. 

    > Note: 
    > 
    > Please note the slashes and use the same while replacing with new path.

- In this edit, you just have to uncomment. In this case, remove the semicolon from .dll extensions to activate it. It is as follows:

    ```powershell
    ;extension=php_gd2.dll 
    ;extension=php_mbstring.dll 
    ;extension=php_mysql.dll 
    ;extension=php_mysqli.dll 
    ```

First line enables the PHP image GD library extension. 

Second line enables mbstring, an extension of php used to manage non-ASCII strings.

The Third and forth enables us to use MySQL database where `php_mysql` is for backward compatibility and `php_mysqli` is for providing latest database API connectivity.

Save the php.ini file. 

### A.2  Adding PHP Environmental Variables in the System path. 

Go to your `Start Menu Icon`->`Control Panel`->`System`->`Advanced System Settings`. Then go to `Advanced` tab, Click on the `Environmental Variables` button. Inside `System variables` select `PATH` variable and append at last the path of PHP folder, in our case,C:\server\php; 

> Note: Dont't forget the semicolon

OR

Right click on `My Computer` -> `Properties` -> `Advanced` -> `Environmental variables` -> `System variables` -> `Path`. Append 
`C:\server\php;` at the end of the line.

### A.3 Reboot your system

You should reboot the system after setting up the Path variable. 

>> Warning: If you move on past to this point without rebooting, you might face issue of Apache HTTP server connections your mySQL extensions. 

With completion of PHP configuration, let's move onto configuring Apache HTTP server.  

## 2. Install and configure Apache HTTP Server

Before starting for actual configuration, you need to know two servers developed by apache software foundation: Apache Tomcat and Apache HTTP. We'll use Apache HTTP server for this setup.

### 2.1 Configure Apache HTTP conf file

Now navigate to `C:\server\Apache\conf`. Now, brace yourself. We have five Edits in this file. No big deal, pretty simple. Just search and replace text.

#### 2.1.1 Uncomment modules library

Search for

`#LoadModule rewrite_module modules/mod_rewrite.so`

Replace with

```
LoadModule rewrite_module modules/mod_rewrite.so 
```

#### 2.1.2 Add PHP module library and setup folder

Add the following below the previous edit.

```
#PHP5LoadModule php5_module "C:/server/php/php5apache2_2.dll" 
```
```
PHPIniDir "C:/server/php"
```

#### 2.1.3 Add PHP supported extensions

Search for

`AddType application/x-gzip .gz .tgz`

Below to this line, add the following lines:  
```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```

> Note: Don't add hash `#` symbol at starting of these two lines.

#### 2.1.4 Add web based languages file extensions

Search for 

`DirectoryIndex index.html`

replace with
```
DirectoryIndex index.html index.php index.py index.pl index.shtml
```

#### 2.1.5 

Search for

`#Include conf/extra/httpd-vhosts.conf`

Replace with
```
Include conf/extra/httpd-vhosts.conf
```

### 2.2 Virtualhost Setup
Now navigate to `C:\server\Apache\conf\extra` and edit `httpd-vhosts.conf`. Replace all the text inside of `httpd-vhosts.conf` with following XML code:

```xml
<virtualhost *:80> 
DocumentRoot "C:/Server/www/myserver.dev/public_html"  ServerName myserver.dev 
ServerAlias www.myserver.dev 
<directory "C:/Server/www/myserver.dev/public_html">  AllowOverride All 
Options Indexes FollowSymLinks 
Order allow,deny 
Allow from all 
</directory>
</virtualhost> 
```

Now, restart the Apache HTTP server. If you've followed perfectly all steps, you`ll see that Apache has restarted perfectly with 

> httpd.exe: could not reliably determine the server's fully qualified domain name using 127.0.0.1 for servername
Step 4  
Testing our Apache + PHP 
 1. Create Directories to store your web files 
 2. Firstly lets make the required Directories. Create a New Folder inside C:\server.  2. Inside the C:\server folder, create folder called www 
 3. inside C:\server\www\ create myserver.dev 
 4. and then finally create public_html folder inside your C:\server\www\myserver.dev\  
 Follow this structure C:\server\www\myserver.dev\public_html\ 
 This is where you will be putting all your html,script etc files to be accessed by your webserver. 
 2. Create index.php 
 Open up notepad, type in the following code and save the file as index.php inside   C\:server\www\myserver.dev\public_html\ as shown in the above picture.  view sourceprint 

Please note the file name, it is index.php. Many times, Notepad saves it as index.php.txt, while saving, don`t forget to mention the type as All Files, this way Notepad will save it as index.php.  Note that for php 5.3.5,the information about php is given by function php_info.php.

C] Configuring Perl scripts
Now, take the breath of relief. The Perl configuration is very easy. Now, httpd.conf file contains the usual Apache configuration directives that can be enabled by uncommenting a certain line. In case of Python CGI scripts, the line containing the AddHandler directive from the http.conf file must have the next structure:

  
In this way, Apache web server will treat Python and Perl files as CGI scripts. The second modification that must be made to Apache configuration file is the specification of the location of your cgi-bin directory by adding the full path to it in the next line (you must replace C:/apache/cgi-bin with the path of your cgi-bin directory): 

 After you save the http.conf file and restart the Apache web server, you will have support to run Python scripts. You can test if the server configuration was successful with the next example (copy and paste the code in a text file and save it as Hello.pl): 

http://localhost/cgi-bin/Hello.pl 
 Click on the above link, you will receive Hello world message.  
 There is a quite small difference between cgi and Perl scripts.CGI scripts are saved with extension .cgi and sample program for PERL cgi is: 

 Save it as test.cgi and check it: 
http://localhost/cgi-bin/test.cgi 
[D] Configuring python scripting: 
 The same procedure for python script only code is important at start up and save with index.py: 
 Click on the following link and check it:
http://localhost/cgi-bin/index.py 
Now, for CGI scripts: 

 Save with ram.cgi and check the following link: 
http://localhost/cgi-bin/ram.cgi. 
This completes our testing of PHP, Perl, Python scripts configuration with Apache HTTP server.   
