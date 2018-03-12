# NFS client image for docker

```sh
docker run -it --rm \
    --privileged \
    -e SOURCE=${NFS_SERVER_IP}:${NFS_SERVER_EXPORT_PATH} \
    otiai10/nfs-client
```
