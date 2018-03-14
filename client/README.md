# NFS client image for docker

[Docker Hub](https://hub.docker.com/r/otiai10/nfs-client/)

```sh
docker run -it --rm \
    --privileged \
    -e SOURCE=${NFS_SERVER_IP}:${NFS_SERVER_EXPORT_PATH} \
    otiai10/nfs-client
```
