# This container should be used for any/all CLI processes
# including cron, queues, etc.
FROM realpage/php:7.0-fpm
LABEL application="lumen" \
      com.realpage.php.version="7.0" \
      com.realpage.php.type="cli"

# Copy the application files to the container
ADD . /var/www/html

# Get the latest composer
ADD https://getcomposer.org/composer.phar /usr/bin/composer

WORKDIR /var/www/html

# Install Composer
RUN apt-get update && apt-get install -y git zip unzip \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \

    # chown a directory up so that the .composer directory that's created will be included
    && chmod 700 /usr/bin/composer \
    && chown -R www-data:www-data /var/www/ /usr/bin/composer

USER www-data
# parallel dependency installation
RUN composer global require hirak/prestissimo \

    # production-ready dependencies
    && composer install  --no-interaction --no-dev --prefer-dist