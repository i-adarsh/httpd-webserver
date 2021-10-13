# Foobar

Foobar is a Python library for dealing with word pluralization.

## Video Link

[![CodeOps](https://img.youtube.com/vi/wRGM0t-yDro/0.jpg)](https://www.youtube.com/watch?v=wRGM0t-yDro)

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install foobar.

# Installation and Configuring httpd Server

>Installing required packages
>
>```
>sudo yum install git httpd -y
>```
>
>Cloning GitHub Repository
>```
>git clone https://github.com/i-adarsh/httpd-webserver.git
>```
>
>Go inside the directory
>```
>cd httpd-webserver/
>ls
>```
>
>Copying index.html file to /var/www/html
>```
>sudo cp index.html /var/www/html/
>```
>Starting and Enabling the httpd server
>```
>sudo systemctl enable httpd --now
>```
>Check web-server is working or not
>```
>curl "http://you_instance_ip"
>```
>### OR
>
>Open the URL in a web browser
>```
>http://you_instance_ip
>```
>

# Setup Route 53

>Now access the webserver with your domain
>```
>http://codeopsindia.ml
>```



# Configuring SSL

>Installing and enabling required repositories
>
>```
>sudo amazon-linux-extras install epel -y
>
>sudo yum-config-manager --enable epel
>```
>Installing required packages
>```
>sudo yum install certbot -y
>```
>Installing Dependencies
>
>```
>sudo yum install python-certbot-apache -y
>```
>
>Create a configuration file for your domain
>```
>sudo vim /etc/httpd/conf.d/codeops.ml.conf
>```
>Edit accordingly and copy the below lines in this file
>```
><VirtualHost *:80>
 >   ServerName codeopsindia.ml
 >   ServerAlias www.codeopsindia.ml
 >   DocumentRoot /var/www/html
 >   ErrorLog /var/log/httpd/codeops-error.log
 >   CustomLog /var/log/httpd/codeops-access.log combined
></VirtualHost>
>```
>
>Now, let's create the SSL certificates for your server
>```
>sudo letsencrypt --renew-by-default
>```
>
>Edit and paste the below lines in the configuration file
>
>```
><VirtualHost *:443>
 >   ServerName codeopsindia.ml
 >   DocumentRoot /var/www/html
 >   ServerAlias www.codeopsindia.ml
 >   DocumentRoot /var/www/html
 >   ErrorLog /var/log/httpd/codeops-error.log
 >   CustomLog /var/log/httpd/codeops-access.log combined
 >
 >   # Example SSL configuration
 >   SSLEngine on
 >   SSLProtocol all -SSLv2
 >   SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5
 >   SSLCertificateFile /etc/letsencrypt/live/codeopsindia.ml/fullchain.pem
 >   SSLCertificateKeyFile /etc/letsencrypt/live/codeopsindia.ml/privkey.pem
> </VirtualHost>
>```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
