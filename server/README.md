# NFS server image for docker

Wake the server up

```sh
% docker run \
  -it --rm --privileged \
  -p 111:111/tcp -p 111:111/udp \
  -p 2049:2049/tcp -p 2049:2049/udp \
  --name nfs-server \
  otiai10/nfs-server
```

Mount from client

```sh
% sudo docker inspect \
  --format "{{.NetworkSettings.IPAddress}}" \
  nfs-server
# Get IP Address of the nfs-server docker container

% mkdir foobar
% sudo mount \
  -t nfs \
  -o nfsvers=4,proto=tcp \
  ${IPAddress}:/ \
  ./foobar
```
