FROM wordpress

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN sed -i 's/\(security\|deb\).debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update && apt-get dist-upgrade -y \
        && apt-get install -y --assume-yes apt-utils net-tools wget vim htop \
        && apt-get autoremove -y \
        && apt-get autoclean -y

WORKDIR /var/www/html
