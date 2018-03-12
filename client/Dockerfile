FROM debian:latest

LABEL maintainer="Hiromu OCHIAI<otiai10@gmail.com>"

RUN apt-get update -qq
RUN apt-get install -y \
    nfs-common

ENV SOURCE=192.168.0.1:/root/export
ENV MOUNTPOINT=/root/mountpoint
RUN mkdir -p ${MOUNTPOINT}

CMD mount ${SOURCE} ${MOUNTPOINT} ; bash
