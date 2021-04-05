FROM centos:7
MAINTAINER Karim Baydon

RUN yum -y update

RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
   yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
   yum -y install openssl nginx git php-pecl-xdebug.x86_64 && \
   yum -y clean all

RUN yum-config-manager --enable remi-php70 && \
   yum -y install php php-xml php-pcre php-spl php-pdo php-mysql php-mcrypt php-gd \
   php-mbstring php-openssl php-json php-curl php-dom php-iconv php-simplexml php-fpm \
   php-soap

RUN cd /tmp && \
   php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
   php composer-setup.php --install-dir=/usr/bin --filename=composer

RUN echo $'\
xdebug.remote_enable=1 \n\
xdebug.remote_host=host.docker.internal \n\
xdebug.remote_port=10000 \n\
xdebug.remote_autostart=0 \n\
xdebug.remote_connect_back=0 \n\
xdebug.profiler_enable_trigger=On \n\
xdebug.profiler_output_dir=/tmp \n\
' > /etc/php.d/xdebug.ini

WORKDIR /usr/share/nginx/html