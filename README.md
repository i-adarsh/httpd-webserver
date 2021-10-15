# Configure httpd webserver with Route 53 and SSL

In this video, I have shown that how we can configure an httpd web server on AWS EC2 instance and then connect it with Route 53 and then enable SSL

## Video Link

>[![CodeOps](https://img.youtube.com/vi/9HNPMq8V2ms/0.jpg)](https://www.youtube.com/watch?v=9HNPMq8V2ms)

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
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/ip.png?raw=true)
>

# Setup Route 53

>Go to Route 53 in AWS and Click on DNS Management
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/select_dns.png?raw=true)
>
>Enter your domain name
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/enter_domain_name.png?raw=true)
>
> Your Dashboard will look like this
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/Screenshot%202021-10-14%20at%2012.22.58%20AM.png?raw=true)
>
> Now we have to create a record for attaching our instance with the domain
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/create_record.png?raw=true)
>
> Insert record for your domain
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/insert_A.png?raw=true)
>
> Create an alias for our domain
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/insert_www.png?raw=true)
>
> Your final Dashboard will look like this
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/final.png?raw=true)
>
> Replace your Nameservers of the domain with the newly obtained nameservers
>
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/freenom_register.png?raw=true)
>
>Now access the webserver with your domain
>
>```
>http://codeopsindia.ml
>```
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/not_secure.png?raw=true)
>

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
>Now access the webserver with your domain
>
>```
>https://codeopsindia.ml
>```
>![alt text](https://github.com/i-adarsh/httpd-webserver/blob/main/secure.png?raw=true)
>

## Contributing
>[Adarsh Kumar](https://github.com/i-adarsh)
>

## License
>[MIT](https://choosealicense.com/licenses/mit/)
