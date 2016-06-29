# This container should be used for any/all CLI processes
# including cron, queues, etc.
FROM realpage/php:7.0-cli
LABEL application="lumen" \
      com.realpage.php.version="7.0" \
      com.realpage.php.type="cli"

# Copy the application files to the container
ADD . /var/www/html

WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y git zip unzip cron \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \

    # Schedule in the crontab
#    && echo "*       *       *       *       *       php /var/www/html/artisan schedule:run" > /etc/crontabs/www-data

# Install Composer
RUN php /var/www/html/infrastructure/install_composer.php
# parallel dependency installation
RUN composer global require hirak/prestissimo \
    # production-ready dependencies
    && composer install  --no-interaction --no-dev --prefer-dist \
