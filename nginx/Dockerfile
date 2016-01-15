FROM yaoyi/ubuntu:14.04
RUN wget -O /tmp/nginx.tar.gz http://nginx.org/download/nginx-1.8.0.tar.gz
RUN cd /tmp/ && tar -xvf nginx.tar.gz -C /usr/local/src/
RUN rm /tmp/nginx.tar.gz
RUN apt-get install -y gcc make libpcre3-dev zlib1g-dev
RUN cd /usr/local/src/nginx-1.8.0/ && ./configure --prefix=/usr/local/  && make && make install
RUN sed -i "1adaemon off;" /usr/local/conf/nginx.conf
EXPOSE 80
CMD /usr/local/sbin/nginx
