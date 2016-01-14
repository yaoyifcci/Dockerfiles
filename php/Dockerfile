FROM yaoyi/ubuntu:14.04
ENV LANG "en_US.UTF-8"

### install dependen packages
RUN apt-get install -y wget curl gcc make libxml2-dev libcurl3-dev libgd-dev libgd-dev
RUN apt-get install -y libmemcached-dev autoconf
RUN useradd www

### install php
RUN wget -O /tmp/phpsrc.tar.gz http://cn2.php.net/distributions/php-5.4.45.tar.gz
RUN tar -xvf /tmp/phpsrc.tar.gz -C /usr/local/src/
RUN rm /tmp/phpsrc.tar.gz
RUN /usr/local/src/php-5.4.45/configure --prefix=/usr/local/ --with-config-file-path=/etc/ --with-curl --enable-fpm --enable-mysqlnd --with-mysql --with-mysqli --with-pdo-mysql --enable-mbstring --with-fpm-user=www --with-fpm-group=www
RUN cp /usr/local/src/php-5.4.45/php.ini-production /etc/php.ini
RUN cd /usr/local/src/php-5.4.45/
RUN make -j `cat /proc/cpuinfo |grep 'core id'|wc -l`
RUN make install

### config php-fpm
RUN mkdir -p /var/log/php
ADD php-fpm.conf /usr/local/etc/php-fpm.conf 

### install memcached
RUN wget -O /tmp/php-memcached.tgz http://pecl.php.net/get/memcached-2.2.0.tgz
RUN tar -xvf /tmp/php-memcached.tgz -C /usr/local/src/php-5.4.45/ext/
RUN rm /tmp/php-memcached.tgz
RUN cd /usr/local/src/php-5.4.45/ext/memcached-2.2.0 && phpize
RUN /usr/local/src/php-5.4.45/ext/memcached-2.2.0/configure --disable-memcached-sasl

#RUN cd /usr/local/src/php-5.4.45/ext/memcached
RUN make -j `cat /proc/cpuinfo |grep 'core id'|wc -l`
RUN make install
RUN echo "extension=memcached.so">>/etc/php.ini

### install redis
RUN pecl install redis
RUN echo "extension=redis.so">>/etc/php.ini

### install igbinary
RUN pecl install igbinary
RUN echo "extension=igbinary.so">>/etc/php.ini

### install gearman lib
RUN apt-get install -y libgearman-dev
RUN pecl install gearman
RUN echo "extension=gearman.so">>/etc/php.ini

### install librabbitmq
RUN wget -O /tmp/librabbitmq.zip https://codeload.github.com/alanxz/rabbitmq-c/zip/v0.7.1
RUN apt-get install -y unzip cmake
RUN cd /tmp/ && unzip librabbitmq.zip
RUN wget -O /tmp/codegen.zip https://codeload.github.com/rabbitmq/rabbitmq-codegen/zip/0a95a69f86cdc2b538f4c58241840563fe4ccf4c
RUN cd /tmp/ && unzip codegen.zip
RUN mv /tmp/rabbitmq-codegen-0a95a69f86cdc2b538f4c58241840563fe4ccf4c/* /tmp/rabbitmq-c-0.7.1/codegen
RUN rm /tmp/codegen.zip /tmp/librabbitmq.zip
RUN mkdir -p /tmp/rabbitmq-c-0.7.1/build/
RUN cd /tmp/rabbitmq-c-0.7.1/build && cmake .. && cmake --build . && cmake -DCMAKE_INSTALL_PREFIX=/usr/ .. && cmake --build . --target install

### install amqp
RUN wget -O /tmp/php-amqp.tgz http://pecl.php.net/get/amqp-1.6.1.tgz
RUN cd /tmp/ && tar -xvf php-amqp.tgz -C /usr/local/src/php-5.4.45/ext/
RUN rm /tmp/php-amqp.tgz
RUN cd /usr/local/src/php-5.4.45/ext/amqp-1.6.1/ && phpize && ./configure && make && make install
RUN echo "extension=amqp.so">>/etc/php.ini


### set php.ini
RUN sed -i "s/^;date.timezone =/date.timezone = Asia\/Shanghai/" /etc/php.ini
