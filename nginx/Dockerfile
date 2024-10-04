FROM nginx:latest

# Install nginx extras and clean up to reduce image size
RUN apt-get update && apt-get install -y nginx-extras


# Forward request and error logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# Remove the default nginx.conf
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom nginx.conf
COPY nginx.conf /etc/nginx