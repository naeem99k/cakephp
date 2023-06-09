# Start from a base image with PHP and Apache
FROM php:8.2-apache

# Install dependencies
RUN apt-get update && apt-get upgrade -y \
    libicu-dev

# Install extensions
RUN docker-php-ext-configure intl \
    && docker-php-ext-install pdo_mysql intl

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory
WORKDIR /var/www/html

# Copy application source
COPY . /var/www/html/

# Change ownership of our applications
RUN chown -R www-data:www-data /var/www/html

# Enable mod_rewrite
RUN a2enmod rewrite

# Install PHP dependencies
RUN composer install

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]