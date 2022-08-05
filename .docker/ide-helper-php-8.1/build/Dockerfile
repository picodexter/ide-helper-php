FROM php:8.1-cli

ARG APPLICATION_DIRECTORY=/var/www/application

RUN echo '[IMAGE BUILD] Starting ...' \
    && echo '[-] Updating Aptitude package cache ...' \
    && apt-get update \
    && echo '[-] Installing system package dependencies ...' \
    && apt-get install -y git unzip \
    && echo '[-] Clearing Aptitude package cache ...' \
    && rm -rf /var/lib/apt/lists/* \
    && echo '[-] Installing Composer ...' \
    && (php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer) \
    && echo '[-] Installing PHP CS Fixer ...' \
    && composer global require friendsofphp/php-cs-fixer \
    && echo '[-] Creating alias for PHP CS Fixer executable ...' \
    && ln -s /root/.composer/vendor/bin/php-cs-fixer /usr/local/bin/ \
    && echo '[-] Installing PHP_CodeSniffer ...' \
    && composer global require squizlabs/php_codesniffer \
    && echo '[-] Creating alias for PHP_CodeSniffer executable ...' \
    && ln -s /root/.composer/vendor/bin/phpcs /usr/local/bin/ \
    && echo '[-] Installing PHPMD ...' \
    && composer global require phpmd/phpmd \
    && echo '[-] Creating alias for PHPMD executable ...' \
    && ln -s /root/.composer/vendor/bin/phpmd /usr/local/bin/ \
    && echo '[-] Installing PHPStan ...' \
    && composer global require phpstan/phpstan \
    && echo '[-] Creating alias for PHPStan executable ...' \
    && ln -s /root/.composer/vendor/bin/phpstan /usr/local/bin/ \
    && echo '[-] Installing Psalm ...' \
    && composer global require vimeo/psalm \
    && echo '[-] Creating alias for Psalm executable ...' \
    && ln -s /root/.composer/vendor/bin/psalm /usr/local/bin/ \
    && echo '[-] Installing Xdebug ...' \
    && pecl install xdebug \
    && echo '[-] Creating application directory ...' \
    && mkdir "${APPLICATION_DIRECTORY}" \
    && echo '[-] Setting permissions for directory ...' \
    && chown www-data:www-data "${APPLICATION_DIRECTORY}" \
    && echo '[-] Changing working directory to application directory ...'

WORKDIR "${APPLICATION_DIRECTORY}"

RUN echo '[IMAGE BUILD] Finished.'
