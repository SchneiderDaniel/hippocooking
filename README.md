
docker-compose run --rm certbot certonly --webroot --webroot-path=/var/www/certbot -d hippocooking.com -d www.hippocooking.com



docker-compose exec certbot /bin/sh
certbot certonly --standalone -d hippocooking.com -d www.hippocooking.com

certbot certonly --standalone -d example.com -d www.example.com