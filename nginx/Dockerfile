FROM nginx:latest

# Install prerequisites and nginx extras
RUN apt-get update && apt-get install -y \
    curl \
    gnupg2 \
    lsb-release \
    && echo "deb http://nginx.org/packages/$(lsb_release -cs)/nginx/ $(lsb_release -cs) nginx" > /etc/apt/sources.list.d/nginx.list \
    && curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add - \
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