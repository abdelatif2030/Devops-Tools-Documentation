# Use a supported PHP version with Apache
FROM php:8.2-apache

# Set working directory
WORKDIR /var/www/html

# Copy app files
COPY ./comingsoon /var/www/html

# Update and install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpng-dev \
    zlib1g-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    curl \
    unzip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql mysqli zip \
    && docker-php-source delete \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && chown -R www-data:www-data /var/www/html

# Expose port 80
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]