FROM php:fpm as base

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV php_env dev

RUN sed -i 's/\(security\|deb\).debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update && apt-get dist-upgrade -y \
        && apt-get install -y --assume-yes git unzip apt-utils libpng-dev net-tools wget vim htop procps openssh-server libgmp-dev \
        && apt-get autoremove -y \
        && apt-get autoclean -y \
	&& docker-php-ext-install exif gd pdo_mysql opcache mysqli gmp

COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    	&& mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" \
	&& kill -USR2 1 \
	&& echo "alias ll='ls $LS_OPTIONS -l --color=auto' 2>/dev/null" >> ~/.bashrc \
	&& echo "alias l.='ls $LS_OPTIONS -d .* --color=auto' 2>/dev/null" >> ~/.bashrc \
	&& echo "alias ls='ls $LS_OPTIONS --color=auto' 2>/dev/null" >> ~/.bashrc \
        && /bin/bash -c "source ~/.bashrc"


