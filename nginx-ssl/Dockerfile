FROM yaoyi/nginx
ADD nginx.conf /nginx/conf/nginx.conf
EXPOSE 443
VOLUME /nginx/logs
VOLUME /nginx/server.d/
VOLUME /nginx/cert.d/
ENTRYPOINT /nginx/sbin/nginx
