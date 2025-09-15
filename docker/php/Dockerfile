FROM php:8.2-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    libpq-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www

# Copy existing application directory contents
COPY . /var/www

# Ensure permissions
RUN chown -R www-data:www-data /var/www

# Expose port (optional)
EXPOSE 9000

RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache && \
    chmod -R 775 /var/www/storage /var/www/bootstrap/cache && \
    php artisan key:generate