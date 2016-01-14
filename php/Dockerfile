FROM yaoyi/ubuntu:14.04
ENV LANG "en_US.UTF-8"
RUN apt-get install -y wget curl gcc make libxml2-dev libcurl3-dev libgd-dev libgd-dev 
RUN useradd www
RUN wget -O /tmp/phpsrc.tar.gz http://cn2.php.net/distributions/php-5.4.45.tar.gz
RUN tar -xvf /tmp/phpsrc.tar.gz -C /usr/local/src/
RUN rm /tmp/phpsrc.tar.gz
RUN /usr/local/src/php-5.4.45/configure --prefix=/usr/local/ --with-curl --enable-fpm --enable-mysqlnd --with-mysql --with-mysqli --with-pdo-mysql --enable-mbstring --with-fpm-user=www --with-fpm-group=www
RUN cp /usr/local/src/php-5.4.45/php.ini-production /etc/php.ini
RUN xargs make -j `cat /proc/cpuinfo |grep 'core id'|wc -l`
RUN make install
