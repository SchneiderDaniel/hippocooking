# Use the official NGINX base image
FROM nginx:1.22.1

# Install the nginx-extras package
RUN apt-get update && \
    apt-get install -y nginx-extras && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy custom NGINX configuration (if any)
# COPY ./my-nginx.conf /etc/nginx/nginx.conf

# Expose HTTP and HTTPS ports
EXPOSE 80 443

