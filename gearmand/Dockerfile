FROM debian:8.2
RUN apt-get update -y
RUN apt-get install -y gearman
EXPOSE 4730
CMD gearmand -L 0.0.0.0 -p 4730 --verbose INFO
