FROM yaoyi/ubuntu:14.04
RUN wget -O /tmp/nginx.tar.gz http://nginx.org/download/nginx-1.8.0.tar.gz
WORKDIR /tmp/
RUN mkdir /src/
RUN tar -xvf nginx.tar.gz -C /src/ && rm /tmp/nginx.tar.gz
RUN apt-get update && apt-get install -y gcc make libpcre3-dev zlib1g-dev libssl-dev openssl
WORKDIR /src/nginx-1.8.0/
RUN ./configure --prefix=/nginx/ --with-http_ssl_module  && make && make install
COPY nginx.conf /nginx/conf/nginx.conf
VOLUME /nginx/conf/server.d/
VOLUME /nginx/logs/
EXPOSE 80
EXPOSE 443
ENTRYPOINT /nginx/sbin/nginx
