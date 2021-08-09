# CONFIGURE YOUR OWN WAMP Server

## 1. INSTALL & CONFIGURE PHP

`Step 1:`

At the time of writing this guide, PHP 8.0.9 is latest stable version available.Download preferred PHP binary zip file from https://windows.php.net. There are two types of zip files available: *Thread Safe* and *Non-thread Safe*. We'll use `thread safe version` for our guide. 

To know more about difference, visit [Microsoft Docs](https://docs.microsoft.com/en-us/iis/application-frameworks/install-and-configure-php-on-iis/install-and-configure-php).

Open the zip file & Extract all your files to C:\server\php. Navigate to C:\server\php 

`Step 2:`

Rename php.ini- file. Search for the file, php.ini-development and rename it to php.ini 

`Step 3:`
EDIT php.ini. Open up php.ini using any text-editor.(Notepad++,Preferably Dreamweaver).  There are 2 edits in this file 
->Edit 1 
Find extension_dir = "./" and replace it with (Please note the slashes) 
extension_dir = "C:/server/php/ext" and remember to remove semicolon(;) at its starting. ->Edit 2 
Now in the following edit, you just have to uncomment (by removing the “; – semicolon”) from the extension to activate it. So here are the extensions to be uncommented. Search for each one them and remove the semicolon (;) 
;extension=php_gd2.dll 
;extension=php_mbstring.dll 
;extension=php_mysql.dll 
;extension=php_mysqli.dll 
The First extension enables the Image GD library of PHP. The Second enables mbstring. The Third and forth enables us to use MySQL database. 
Save the php.ini file. 

`Step 4:`

Adding PHP Environmental Variables in the System path. 
Great! Now we have to add tell the computer to start php every time the computer reboots.
 So, Navigate to your Start->Control Panel->System->Advanced System Settings then go to the advanced tab, Click on the Environmental Variables button, then scroll down in system variables to find PATH, Edit it Add the following Code to it, [ C:\server\php; ] 
 OR 
 Right click on My Computer->Properties->Advanced->environmental variables->System variables->Path. Add C:\server\php; at the starting. 
Step 5: 
 You MUST MUST MUST reboot a windows box after setting the Path variable (step 2). If you move on past that point without rebooting – logging off is NOT enough – apache will have trouble finding your mySQL extensions. 
Finally, Step 2 is over !. Now we have PHP configured. Lets move on to configuring Apache.  [B] Configuring Apache HTTP Server 2.2.17  
 Before this, you need to know there are two servers developed by apache software foundation: apache tomcat server & apache http server. In year 2011,

## Apache Tomcat 7.0.6 and Apache HTTP server 2.2.17. 

`Step 1:`

Now navigate to C:\server\Apache\conf 
 OK, brace yourself; we got 5 Edits in this file. No big deal,  
Pretty simple search and replace text. 
 1 
 Search for-> 
 #LoadModule rewrite_module modules/mod_rewrite.so 
 Replace with-> 
 LoadModule rewrite_module modules/mod_rewrite.so 
 Edit 2 
 Add the following below the previous edit-> 
 #PHP5 
 LoadModule php5_module "C:/server/php/php5apache2_2.dll" 
 PHPIniDir "C:/server/php"
Edit 3 
 Search-> 
 AddType application/x-gzip .gz .tgz 
 Add the following below the searched line-> 
 AddType application/x-httpd-php .php 
 AddType application/x-httpd-php-source .phps 
 Note: Don't add hash(#) symbol at starting of these two lines.  Edit 4 
 Search for-> 
 DirectoryIndex index.html 
 Replace with-> 
 DirectoryIndex index.html index.php index.py index.pl index.shtml  Edit 5 
 Search for-> 
 #Include conf/extra/httpd-vhosts.conf 
Replace with->  
 Include conf/extra/httpd-vhosts.conf 
 Step 2 
 Now navigate to C:\server\Apache\conf\extra  
 Edit httpd-vhosts.conf 
 Step 3  
 Replace all the text inside with 
 <virtualhost *:80> 
 DocumentRoot "C:/Server/www/myserver.dev/public_html"  ServerName myserver.dev 
 ServerAlias www.myserver.dev 
 <directory "C:/Server/www/myserver.dev/public_html">  AllowOverride All 
 Options Indexes FollowSymLinks 
 Order allow,deny 
 Allow from all 
 </directory>
 </virtualhost> 
 Now,Restart the Apache Webserver 
 If you have followed perfectly you`ll see that Apache has restarted perfectly with some error message do not take it into consideration. 
Step 4  
Testing our Apache + PHP 
 1. Create Directories to store your web files 
 1. Firstly lets make the required Directories. Create a New Folder inside C:\server.  2. Inside the C:\server folder, create folder called www 
 3. inside C:\server\www\ create myserver.dev 
 4. and then finally create public_html folder inside your C:\server\www\myserver.dev\  
 Follow this structure C:\server\www\myserver.dev\public_html\ 
 This is where you will be putting all your html,script etc files to be accessed by your webserver. 
 2. Create index.php 
 Open up notepad, type in the following code and save the file as index.php inside   C\:server\www\myserver.dev\public_html\ as shown in the above picture.  view sourceprint 

Please note the file name, it is index.php. Many times, Notepad saves it as index.php.txt, while saving, don`t forget to mention the type as All Files, this way Notepad will save it as index.php.  Note that for php 5.3.5,the information about php is given by function php_info.php.

[C] Configuring Perl scripts: 
Now, take the breath of relief. The Perl configuration is very easy. Now, httpd.conf file contains the usual Apache configuration directives that can be enabled by uncommenting a certain line. In case of Python CGI scripts, the line containing the AddHandler directive from the http.conf file must have the next structure:

  
In this way, Apache web server will treat Python and Perl files as CGI scripts. The second modification that must be made to Apache configuration file is the specification of the location of your cgi-bin directory by adding the full path to it in the next line (you must replace C:/apache/cgi-bin with the path of your cgi-bin directory): 

 After you save the http.conf file and restart the Apache web server, you will have support to run Python scripts. You can test if the server configuration was successful with the next example (copy and paste the code in a text file and save it as Hello.pl): 

http://localhost/cgi-bin/Hello.pl 
 Click on the above link, you will receive Hello world message.  
 There is a quite small difference between cgi & Perl scripts.CGI scripts are saved with extension .cgi and sample program for PERL cgi is: 

 Save it as test.cgi and check it: 
http://localhost/cgi-bin/test.cgi 
[D] Configuring python scripting: 
 The same procedure for python script only code is important at start up & save with index.py: 
 Click on the following link and check it:
http://localhost/cgi-bin/index.py 
Now, for CGI scripts: 

 Save with ram.cgi and check the following link: 
http://localhost/cgi-bin/ram.cgi. 
This completes our testing of PHP, Perl, Python scripts configuration with Apache HTTP server.   
