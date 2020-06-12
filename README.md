# PXE Docker container

PXE service Docker container based on dnsmasq network service.

# Cleanup

```
docker rm --force pxe-dnsmasq
```

```
docker rmi pxe-dnsmasq
```

# Build

```
docker build --tag pxe-dnsmasq .
```

# Run

```
docker run \
    --rm \
    --name pxe-dnsmasq \
    --net host pxe-dnsmasq \
    -e "E_INT=$(ip -o -4 route show to default | awk '{print $5}')" \
    -e "E_ADD=$(hostname -I | awk '{print $1}')"
```
