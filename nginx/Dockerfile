# Stage 1: Build Nginx with extras
FROM debian:bullseye-slim AS builder

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y \
    build-essential \
    libpcre3-dev \
    libssl-dev \
    zlib1g-dev \
    wget \
    curl \
    gnupg2

# Install Nginx with extras
RUN wget http://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    echo "deb http://nginx.org/packages/mainline/debian/ bullseye nginx" >> /etc/apt/sources.list && \
    echo "deb-src http://nginx.org/packages/mainline/debian/ bullseye nginx" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y nginx-extras && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Stage 2: Copy the built Nginx from the builder stage
FROM debian:bullseye-slim

# Install the Nginx and other required packages
COPY --from=builder /usr/sbin/nginx /usr/sbin/nginx
COPY --from=builder /etc/nginx /etc/nginx
COPY --from=builder /usr/share/nginx/html /usr/share/nginx/html
COPY --from=builder /var/log/nginx /var/log/nginx

# Expose port 80
EXPOSE 80

# Copy your custom Nginx configuration file (nginx.conf)
COPY nginx.conf /etc/nginx
