FROM php:8.3-fpm

# Instalar dependências
RUN apt-get update && apt-get install -y \
    libzip-dev \
    libpng-dev \
    libpq-dev \
    postgresql-client \
    unzip \
    git \
    curl \
    zip \
    npm \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Instalar extensões PHP
RUN docker-php-ext-install pdo_pgsql bcmath gd zip

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
