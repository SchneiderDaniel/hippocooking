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
RUN curl -fsSL https://nginx.org/keys/nginx_signing.key | gpg --dearmor -o /etc/apt/trusted.gpg.d/nginx_signing.gpg && \
    echo "deb http://nginx.org/packages/mainline/debian/ bullseye nginx" >> /etc/apt/sources.list && \
    echo "deb-src http://nginx.org/packages/mainline/debian/ bullseye nginx" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y nginx-extras && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Stage 2: Use slim image for final Nginx
FROM debian:bullseye-slim

# Install required directories and Nginx dependencies
RUN apt-get update && apt-get install -y libpcre3 zlib1g libssl1.1 && \
    mkdir -p /var/run/nginx /var/cache/nginx /etc/nginx/modules-enabled

# Copy Nginx binaries, config, and modules from the builder stage
COPY --from=builder /usr/sbin/nginx /usr/sbin/nginx
COPY --from=builder /etc/nginx /etc/nginx
COPY --from=builder /usr/share/nginx/html /usr/share/nginx/html
COPY --from=builder /var/log/nginx /var/log/nginx

# Replace with the correct path you identified (example: /usr/share/nginx/modules)
COPY --from=builder /usr/share/nginx/modules /usr/share/nginx/modules  # Add this line to copy the modules
COPY --from=builder /etc/nginx/modules-enabled /etc/nginx/modules-enabled  # Add this line to copy the module config files

CMD ["nginx", "-g", "daemon off;"]
