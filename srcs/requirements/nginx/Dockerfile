FROM    debian:bullseye

WORKDIR /nginx/

# Install nginx and openssl (for self-signed SSL certificates)
RUN apt-get update && \
    apt-get install -y nginx openssl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp

# Generate self-signed SSL certificate (change details as needed)
RUN mkdir -p /etc/ssl/certs /etc/ssl/private && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/nginx.key \
    -out /etc/ssl/certs/nginx.crt \
    -subj "/C=FR/ST=IDF/L=Paris/O=42/OU=student/CN=localhost"

# Copy custom nginx config file
COPY ./nginx.conf /etc/nginx/nginx.conf

# Set up web root for WordPress (just as a placeholder; real WordPress files should be mounted with a volume)
RUN mkdir -p /var/www/wordpress

# Expose HTTP and HTTPS ports
EXPOSE 80 443

# Start nginx in foreground (important for Docker)
CMD ["nginx", "-g", "daemon off;"]