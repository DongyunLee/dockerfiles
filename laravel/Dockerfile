FROM php:fpm as base

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV php_env dev

RUN sed -i 's/\(security\|deb\).debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update && apt-get dist-upgrade -y \
        && apt-get install -y -qq git unzip apt-utils net-tools wget vim htop procps openssh-server libmcrypt-dev libjpeg-dev libpng-dev libfreetype6-dev libbz2-dev libzip-dev \
	   libonig-dev \
	   libxml2-dev \
        && apt-get autoremove -y \
        && apt-get autoclean -y 

RUN pecl install mcrypt-1.0.3 \
	&& docker-php-ext-enable mcrypt \
	&& docker-php-ext-install pdo pdo_mysql opcache bcmath zip gd pcntl fileinfo json mbstring tokenizer xml

COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    	&& mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" \
	&& kill -USR2 1 \
	&& echo "alias ll='ls $LS_OPTIONS -l --color=auto' 2>/dev/null" >> ~/.bashrc \
	&& echo "alias l.='ls $LS_OPTIONS -d .* --color=auto' 2>/dev/null" >> ~/.bashrc \
	&& echo "alias ls='ls $LS_OPTIONS --color=auto' 2>/dev/null" >> ~/.bashrc \
        && /bin/bash -c "source ~/.bashrc"

# Install Node
RUN apt-get update &&\
    apt-get install -y --no-install-recommends gnupg &&\
    curl -sL https://deb.nodesource.com/setup_15.x | bash - &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends nodejs &&\
    npm config set registry https://registry.npm.taobao.org --global &&\
    npm install -g npm &&\
    npm install --global gulp-cli

WORKDIR /var/www/html
