# fog-server
fog-server for arm64

## In the file [Dockerfile](Dockerfile):
We are simply updating the server.

## In the file [docker-entrypoint.sh](docker-entrypoint.sh):

If you want to change default port for the webserver:

Uncomment these lines
```sh
sh -c '/bin/sed -i "s/^Listen 80.*/Listen 8083/g" /etc/apache2/ports.conf'
sh -c '/bin/sed -i "s/Listen 443$/Listen 44383/g" /etc/apache2/ports.conf'
sh -c '/bin/sed -i "1s/.*/<VirtualHost *>/g" /etc/apache2/sites-enabled/000-default.conf'
sh -c '/bin/sed -i "1s/.*/<VirtualHost *>/g" /etc/apache2/sites-enabled/001-fog.conf'
sh -c '/bin/sed -i "s/192.168.2.3/192.168.2.3:8083/g" /tftpboot/default.ipxe'
```
else, leave these lines alone.

Change these lines with the approiate IP address:

```sh
sh -c '/bin/sed -i "6s/.*/CN = 192.168.2.3/g" /opt/fog/snapins/ssl/req.cnf'
sh -c '/bin/sed -i "10s/.*/DNS.1 = 192.168.2.3/g" /opt/fog/snapins/ssl/req.cnf'
sh -c '/bin/sed -i "4s/.*/DNS.1 = 192.168.2.3/g" /opt/fog/snapins/ssl/ca.cnf'
sh -c "/bin/sed -i '/HOST/ s/\".*\"/\"192.168.2.3\"/g' /var/www/fog/lib/fog/config.class.php"
```

else, leave these lines alone.
