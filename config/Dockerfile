# Comment
FROM centos:6

LABEL Vendor="CentOS"

ENV PHANTOM_JS_VERSION 1.9.7-linux-x86_64

RUN echo 'Estamos comecando a inicializar seu container'
RUN rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
RUN     rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

RUN yum -y update;
RUN yum -y install nodejs acl php56w.x86_64 php56w-xml.x86_64 php56w-pdo.x86_64 php56w-mysql.x86_64 php56w-imap.x86_64 php56w-pecl-xdebug.x86_64 php56w-mcrypt.x86_64 php56w-mbstring.x86_64 php56w-ldap.x86_64 git.x86_64 npm tar.x86_64 bzip2.x86_64 fontconfig freetype freetype-devel fontconfig-devel libstdc++ wget php56w-pecl-memcached.x86_64 php56w-intl.x86_64

RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-1.9.8-linux-x86_64.tar.bz2
RUN mkdir -p /opt/phantomjs
RUN tar -xvjpf  phantomjs-1.9.8-linux-x86_64.tar.bz2
RUN cp -Rfa phantomjs-1.9.8-linux-x86_64/* /opt/phantomjs/
RUN ln -s /opt/phantomjs/bin/phantomjs /usr/bin/phantomjs

RUN npm install bower
RUN curl -sS https://getcomposer.org/installer | php  -- --install-dir=/bin
RUN cp /bin/composer.phar /bin/composer


EXPOSE 80
EXPOSE 9876

ADD httpd/virtualHost.conf /etc/httpd/conf.d/
ADD httpd/httpd.conf /etc/httpd/conf/
ADD httpd-script.sh /httpd-script.sh

ADD .ssh/* /root/.ssh/

RUN mkdir -p /var/www/html && chmod -Rf 777 /var/www/html
RUN chmod -v +x /httpd-script.sh


CMD ["/httpd-script.sh"]




