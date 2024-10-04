FROM debian:bullseye

# Install prerequisites
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    lsb-release \
    apt-utils \
    && rm -rf /var/lib/apt/lists/*

# Add NGINX signing key and repository
RUN curl -fsSL https://nginx.org/keys/nginx_signing.key | tee /usr/share/keyrings/nginx-archive-keyring.gpg > /dev/null \
    && echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/debian/ bullseye nginx" > /etc/apt/sources.list.d/nginx.list \
    && apt-get update \
    && apt-get install -y nginx-extras \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Forward request and error logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# Remove the default nginx.conf
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom nginx.conf
COPY nginx.conf /etc/nginx