# notes
#******linux******
httpd -t
/etc/init.d/httpd start
We need to install two Packages to Configure SSL for Apache VirtualHost i.e.

1. openssl
2. mod_ssl

yum -y install openssl mod_ssl
openssl genrsa -out elinuxbook.key 2048
openssl req -new -key elinuxbook.key -out elinuxbook.csr
openssl x509 -req -days 1095 -in elinuxbook.csr -signkey elinuxbook.key -out elinuxbook.crt
cp elinuxbook.crt /etc/pki/httpd -t
/etc/init.d/httpd start
We need to install two Packages to Configure SSL for Apache VirtualHost i.e.

1. openssl
2. mod_ssl

yum -y install openssl mod_ssl

openssl genrsa -out elinuxbook.key 2048

openssl req -new -key elinuxbook.key -out elinuxbook.csr

openssl x509 -req -days 1095 -in elinuxbook.csr -signkey elinuxbook.key -out elinuxbook.crt

#Copy the elinuxbook.crt to /etc/pki/tls/cert

cp elinuxbook.crt /etc/pki/tls/certs/

#Copy the elinuxbook.key to /etc/pki/tls/private

cp elinuxbook.key /etc/pki/tls/private/

#Copy the elinuxbook.csr to /etc/pki/tls/private

cp elinuxbook.csr /etc/pki/tls/private/tls/certs/

#Configure ssl.conf

#nano /etc/httpd/conf.d/ssl.conf

#now search for SSLCertificateFile

SSLCertificateFile /etc/pki/tls/certs/elinuxbook.crt

#now search for SSLCertificateKeyFile 

SSLCertificateKeyFile /etc/pki/tls/private/elinuxbook.key

#SSL Configuration for VirtualHost

Replace the Port 80 with 443 as Port Number of SSL is 443  and then place below mentioned lines after <VirtualHost 192.168.0.107:443>

# To Enable the SSL Support for this VirtualHost

SSLEngine on

# Path of SSL Certificate File   
 
SSLCertificateFile /etc/pki/tls/certs/elinuxbook.crt

# Path of SSL Certificate Key File  

SSLCertificateKeyFile /etc/pki/tls/private/elinuxbook.key   


/etc/init.d/httpd restart




