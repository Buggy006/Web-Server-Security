# Web-Server-Security
Kode Kloud - System Administrator
### During recent security audit, application security team of xFusionCorp Industries found some security issues with Apache web server on Nautilus App Server 2 server in Stratos DC. They have listed out some security issues that need to be fixed on this server. Please apply the below mentioned security settings:


### a. On Nautilus App Server 1 it was identified that Apache web server is exposing the version number. Make appropriate settings on this server to hide the version number of Apache web server.

### b. There is a website hosted under /var/www/html/news on App Server 1 . It was detected that the directory /news is listing all of its contents while browsing the URL. Disable directory browser listing in Apache config.

### c. Also make sure to restart Apache service after making the changes.

#### First Login to App Server 
  ```
    ssh tony@stapp01
   ```
   #### Go to Apache Conf file and add these lines in end of the conf file.
  ```
    ServerTokens Prod
    ServerSignature Off
    Systemctl restart httpd
  ```  
##### TO Hide Web Server Version Number and Disable the directory Browser , Open Apache Conf File
```
cd /var/www/html/news
vi .htaccess    -Create .htaccess to manage directory configurations
```
##### Add these lines configurations files to .htaccess
```
<Directory /var/www/html/news/>
      Options -Indexes
</Directory>
```
##### While using the .htaccess, make sure that Apache server is enabled for .htaccess for the appropriate directory. In most cases, .htaccess is disabled by default
##### To enable go to /var/www/html directory change Allowoverride None to Allowoverride All.

```
vi /etc/httpd/conf/httpd.conf
<Directory "/var/www/html">   
Allowoverride all .
</Directory>
```
##### This will enable the respective directory annd sub-directories

###### Validate it.

```
curl http:\\stapp01:8080\
```


