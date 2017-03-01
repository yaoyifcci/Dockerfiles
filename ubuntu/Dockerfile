FROM ubuntu:14.04
RUN sed -i "s/archive.ubuntu.com/cn.archive.ubuntu.com/g" /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get install -y wget curl gcc make
