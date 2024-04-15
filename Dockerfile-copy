# Use an official PHP image with the FPM (FastCGI Process Manager) variant
FROM php:7.4-fpm-alpine

# Install dependencies required for Laravel
RUN apk add --no-cache \
    openssl \
    bash \
    nodejs \
    npm \
    git

# Install extensions needed by Laravel
RUN docker-php-ext-install pdo pdo_mysql

# Install Composer globally
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy existing application directory contents
COPY . /var/www/html

# Install all PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Change ownership of our applications
RUN chown -R www-data:www-data /var/www/html

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
