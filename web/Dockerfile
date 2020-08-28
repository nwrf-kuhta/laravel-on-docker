FROM centos:centos7.8.2003
LABEL maintainer="nwrf.kuhta <nwrf.kuhta@gmail.com>"

# Update yum and clean it.
RUN yum -y update \
    && yum clean all

# Install the required packages.
RUN yum -y install \
    gcc \
    gcc-c++ \
    re2c \
    cmake3 \
    libcurl-devel \
    less \
    wget \
    zip \
    unzip \
    vim \
    screen \
    git \
    rsync \
    make

# Update GCC.
RUN yum -y install centos-release-scl-rh \
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SCLo \
    && yum -y install \devtoolset-7-gcc devtoolset-7-gcc-c++ devtoolset-7-binutils \
    && yum-config-manager --disable centos-sclo-rh \
    && mv -f /usr/bin/gcc /usr/bin/gcc_old \
    && ln -s /opt/rh/devtoolset-7/root/usr/bin/gcc /usr/bin/gcc

# install remi.
RUN yum -y install epel-release \
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 \
    && rpm --import http://rpms.famillecollet.com/RPM-GPG-KEY-remi \
    && rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

# Install what you need for PHP.
RUN yum -y install \
    automake \
    autoconf \
    libXpm \
    libpng \
    fontconfig

# Install PHP.
RUN yum -y --enablerepo=epel,remi install \
    php74-php \
    php74-php-fpm \
    php74-php-bcmath \
    php74-php-ctype \
    php74-php-fileinfo \
    php74-php-json \
    php74-php-mbstring \
    php74-php-openssl \
    php74-php-pdo \
    php74-php-tokenizer \
    php74-php-xml \
    php74-php-xmlrpc \
    php74-php-mcrypt \
    php74-php-gd \
    php74-php-mysqlnd \
    php74-php-pecl-mysql \
    php74-php-zip \
    php74-php-intl \
    php74-php-opcache

# Change php-fpm settings.
COPY ./php/php-fpm.d/www.conf /etc/opt/remi/php74/php-fpm.d/www.conf

# Add environment variables for PHP.
ENV PATH=/opt/remi/php74/root/usr/bin:/opt/remi/php74/root/usr/sbin${PATH:+:${PATH}}
ENV LD_LIBRARY_PATH=/opt/remi/php74/root/usr/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
ENV MANPATH=/opt/remi/php74/root/usr/share/man:${MANPATH}

# Copy PHP custom settings.
COPY ./php/php.d/custom-php.ini /etc/opt/remi/php74/php.d/custom-php.ini

# Install composer.
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Install the nginx.
RUN yum -y install nginx

# Remove MariaDB and Install MySQL.
RUN yum -y remove mariadb-libs \
    && rm -rf /var/lib/mysql \
    && rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm \
    && yum -y install --enablerepo=mysql57-community mysql-community-client

# Instal Redis.
RUN yum -y --enablerepo=epel install redis

# Start the process.
COPY ./docker-entrypoint.sh /tmp/docker-entrypoint.sh
CMD ["/sbin/init"]
ENTRYPOINT sh /tmp/docker-entrypoint.sh
