FROM php:8.2-apache

# Set working directory
WORKDIR /var/www/html

# Install system dependencies + clean cache لتقليل الحجم
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libzip-dev \
    zip \
    curl \
    unzip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql mysqli zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy project files
COPY . .

# Set correct permissions
RUN chown -R www-data:www-data /var/www/html

# Enable Apache rewrite (مهم للـ Laravel)
RUN a2enmod rewrite

# Expose port
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]