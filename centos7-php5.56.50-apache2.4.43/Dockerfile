FROM centos:7
MAINTAINER apache2.4.43 with php 5.6.40 power by Mikako
RUN mkdir /stage && cd /stage && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && yum -y install wget && wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo && wget https://mirror.bit.edu.cn/apache//apr/apr-1.7.0.tar.gz && wget https://mirrors.tuna.tsinghua.edu.cn/apache//apr/apr-1.7.0.tar.gz && wget https://mirrors.tuna.tsinghua.edu.cn/apache//httpd/httpd-2.4.46.tar.gz && wget https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz && wget https://www.php.net/distributions/php-5.6.40.tar.gz  && tar xf apr-1.7.0.tar.gz && tar xf apr-1.7.0.tar.gz && tar xf httpd-2.4.46.tar.gz && tar xf pcre-8.44.tar.gz && tar xf php-5.6.40.tar.gz  && yum -y install python-setuptools && easy_install supervisor && yum -y install gcc \
    make \
    gcc-c++ \
    expat-devel \
    zlib-devel \
    freetype-devel \
    libxml2-devel \
    libjpeg-devel \
    libpng-devel \
    perl \
    re2c \
    openssl-devel \
    bzip2-devel \
    libcurl-devel \
    libc-client-devel \
    libmcrypt-devel \
    libxslt-devel \
    bison-devel && cd /stage/apr-1.7.0 && ./configure --prefix=/usr/local/apr && make && make install && cd  /stage/apr-util-1.6.1 && ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr && make && make install && cd /stage/pcre-8.44 && ./configure --prefix=/usr/local/pcre && make && make install && cd /stage/httpd-2.4.43/ && \
    ./configure --prefix=/usr/local/apache2 \
    --with-apr=/usr/local/apr \
    --enable-ssl=sharedSSL \
    --with-apr-util=/usr/local/apr-util \
    --with-pcre=/usr/local/pcre \
    --enable-module=all \
    --enable-expires=shared \
    --enable-speling=shared \
    --enable-rewrite=shared \
    --enable-proxy=shared \
    --enable-deflate=shared \
    && make && make install && cd /stage/php-5.6.40/ && \
    ./configure \
    --prefix=/usr/local/php --with-config-file-path=/etc --with-config-file-scan-dir=/etc/php.d --with-zlib-dir --with-freetype-dir --enable-mbstring --with-libxml-dir=/usr/local/libxml --enable-soap --enable-calendar --with-curl --with-mcrypt --with-gd --disable-rpath --enable-inline-optimization --with-bz2 --with-zlib --enable-sockets --enable-sysvsem --enable-sysvshm --enable-pcntl --enable-mbregex --enable-exif --enable-bcmath --with-mhash --enable-zip --with-pcre-regex --with-mysql --with-pdo-mysql --with-mysqli --with-jpeg-dir --with-png-dir --enable-gd-native-ttf --with-openssl --with-fpm-user=www --with-fpm-group=www --with-libdir=lib64 --enable-ftp --with-imap --with-imap-ssl --with-kerberos --with-gettext --with-xmlrpc --with-xsl --enable-opcache --enable-fpm --enable-xml --enable-shmop --enable-session --enable-ctype --with-iconv-dir --with-iconv --with-apxs2=/usr/local/apache2/bin/apxs && make && make install && rm -rf /stage && rm -rf /usr/local/apache2/conf/httpd.conf && rm -rf /usr/local/apache2/htdocs/* && yum -y remove python-setuptools wget gcc gcc-c++ make && yum clean all && rm -rf /var/lib/yum/yumdb/* 

ADD ./httpd.conf /usr/local/apache2/conf/
ADD supervisor.conf.apache /etc/supervisord.conf.apache
CMD supervisord -c /etc/supervisord.conf.apache
EXPOSE 8080
