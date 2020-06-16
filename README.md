# PXE Docker container

PXE service Docker container based on dnsmasq network service.

# Cleanup

```
docker rm --force pxe-dnsmasq
docker rmi pxe-dnsmasq
```

# Build

```
docker build \
    --network host \
    --build-arg HTTP_PROXY="$http_proxy" \
    --build-arg HTTPS_PROXY="$http_proxy" \
    --build-arg NO_PROXY="$no_proxy" \
    --build-arg http_proxy="$http_proxy" \
    --build-arg https_proxy="$http_proxy" \
    --build-arg no_proxy="$no_proxy" \
    --tag pxe-dnsmasq .
```

# Run

```
docker run \
    --rm \
    --name pxe-dnsmasq \
    --env "E_INT=$(ip -o -4 route show to default | awk '{print $5}')" \
    --env "E_ADD=$(hostname -I | awk '{print $1}')" \
    --cap-add NET_ADMIN \
    --net host pxe-dnsmasq
```
