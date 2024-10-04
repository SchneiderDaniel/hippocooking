# Use the official NGINX base image
FROM nginx:1.22.1

# Install the nginx-extras package
RUN apt-get update && \
    apt-get install -y nginx-extras && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy custom NGINX configuration (if any)
# Replace with our own nginx.conf
COPY nginx.conf /etc/nginx

# Expose HTTP and HTTPS ports
EXPOSE 80 443

