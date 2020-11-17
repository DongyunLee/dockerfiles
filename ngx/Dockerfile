FROM nginx:stable 

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN sed -i 's/\(security\|deb\).debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update && apt-get dist-upgrade -y \
        && apt-get install -y --assume-yes apt-utils net-tools wget vim htop certbot python-certbot-nginx inetutils-ping \
        && apt-get autoremove -y \ 
        && apt-get autoclean -y

RUN echo "alias ll='ls $LS_OPTIONS -l --color=auto' 2>/dev/null" >> ~/.bashrc \
        && echo "alias l.='ls $LS_OPTIONS -d .* --color=auto' 2>/dev/null" >> ~/.bashrc \
        && echo "alias ls='ls $LS_OPTIONS --color=auto' 2>/dev/null" >> ~/.bashrc \
        && /bin/bash -c "source ~/.bashrc"

WORKDIR /etc/nginx
