# This container should be used for any/all CLI processes
# including cron, queues, etc.
FROM realpage/php:7.0-alpine
LABEL application="lumen" \
      com.realpage.php.version="7.0" \
      com.realpage.php.type="cli"

# Copy the application files to the container
ADD . /var/www/html

WORKDIR /var/www/html

# Install Composer dependencies
RUN apk add --update --no-cache git zip unzip \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Composer
RUN php /var/www/html/infrastructure/install_composer.php
# parallel dependency installation
RUN composer global require hirak/prestissimo \
    # production-ready dependencies
    && composer install  --no-interaction --no-dev --optimize-autoloader --prefer-dist \
