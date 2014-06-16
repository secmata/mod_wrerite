mod_wrerite
===========
  
  <IfModule mod_rewrite.c>
      RewriteEngine On
      RewriteBase /my_site/
  
      #Removes access to the system folder by users.
      #Additionally this will allow you to create a System.php controller,
      #previously this would not have been possible.
      #'system' can be replaced if you have renamed your system folder.
      RewriteCond %{REQUEST_URI} ^system.*
      RewriteRule ^(.*)$ /index.php?/$1 [L]
      
      #When your application folder isn't in the system folder
      #This snippet prevents user access to the application folder
      #Submitted by: Fabdrol
      #Rename 'application' to your applications folder name.
      RewriteCond %{REQUEST_URI} ^application.*
      RewriteRule ^(.*)$ /index.php?/$1 [L]
  
      #Checks to see if the user is attempting to access a valid file,
      #such as an image or css document, if this isn't true it sends the
      #request to index.php
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteRule ^(.*)$ index.php?/$1 [L]
      
      </IfModule>
  
      <IfModule !mod_rewrite.c>
          # If we don't have mod_rewrite installed, all 404's
          # can be sent to index.php, and everything works as normal.
          # Submitted by: ElliotHaughin
  
      ErrorDocument 404 /index.php
  </IfModule> 
  
1. my_site\ .htaccess

	=> RewriteBase /my_site/

2. my_site\application\config\autoload.php

	=> $autoload['helper'] = array('url'); 

3. my_site\application\config\config.php 

	=> $config['index_page'] = ''; 
	=> $config['base_url']	= 'http://localhost/my_site'; 

4. http://localhost/my_site/welcome/site

	echo base_url(); 
