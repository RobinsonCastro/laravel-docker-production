FROM php:8.3-fpm

# Instalar dependências
RUN apk update && apk add --no-cache \
    icu-dev \
    zip \
    libzip-dev \
    supervisor \
    && docker-php-ext-install mysqli pdo pdo_mysql zip \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-install pcntl

# Instalar extensões PHP
RUN docker-php-ext-install bcmath gd zip

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Diretório de trabalho
WORKDIR /var/www

# Copiar código
COPY . .

# Instalar dependências PHP
RUN composer install --no-dev --optimize-autoloader

# Permissões
RUN chown -R www-data:www-data storage bootstrap/cache

CMD ["php-fpm", "-F"]
