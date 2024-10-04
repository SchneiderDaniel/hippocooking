
# Intial Setup:

1. create the certbot container and make sure it can connect to port 80. 
```
ports:
- "80:80"
```

2. Go in the container: ```docker-compose exec certbot /bin/sh```
3. Create the cert: ```certbot certonly --standalone -d hippocooking.com -d www.hippocooking.com```
4. Remove the ports again
5. From now on call: ```docker-compose run --rm certbot certonly --webroot --webroot-path=/var/www/certbot -d hippocooking.com -d www.hippocooking.com```
6. go in ``/hippocooking/nginx/ssl-dhparams`` and run: ```openssl dhparam -out dhparam.pem 2048```




