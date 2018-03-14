FROM centos:latest

LABEL maintainer="Hiromu OCHIAI<otiai10@gmail.com>"

ARG MOUNTPOINT="/root/mount"
RUN mkdir -p ${MOUNTPOINT} && chmod 777 ${MOUNTPOINT}

# Install reequired packages
RUN yum install -y nfs-utils

# Place s6-overlay to enable services
ADD https://github.com/just-containers/s6-overlay/releases/download/v1.21.4.0/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C / --exclude="./bin"
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /usr ./bin

RUN mkdir -p /etc/cont-init.d \
    && printf "#!/usr/bin/with-contenv sh\nexportfs -r" >> /etc/cont-init.d/00-config

RUN mkdir -p /etc/services.d/rpcbind \
    && printf "#!/usr/bin/with-contenv sh\nrpcbind -f" >> /etc/services.d/rpcbind/run \
    && chmod 755 /etc/services.d/rpcbind/run \
    && cat /etc/services.d/rpcbind/run

RUN mkdir -p /etc/services.d/mountd \
    && printf "#!/usr/bin/execlineb  -P\nforeground { rpc.nfsd -N 2 -N 3 }\nrpc.mountd -F -N 2 -N 3" >> /etc/services.d/mountd/run \
    && chmod 755 /etc/services.d/mountd/run \
    && cat /etc/services.d/mountd/run

# Expose ports for NFS
EXPOSE 111/udp 111/tcp 2049/udp 2049/tcp

RUN echo "${MOUNTPOINT} *(rw,fsid=0,root_squash,no_subtree_check,insecure)" >> /etc/exports
RUN ls -la /etc/services.d/mountd

# Kick init script of s6-overlay
ENTRYPOINT /init
