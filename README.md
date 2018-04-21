# Minimal docker image for OpenVPN startup

## Prerequirements
Linux, git, Docker

## Clone this repository
```sh
root@host# git clone https://github.com/pavelpatrin/openvpn-docker-minimal.git
root@host# cd openvpn-docker-minimal
```

## Build docker image for your server
```sh
root@host# docker build . -t openvpn \
    --build-arg server_host=yourserver.com \
    --build-arg server_port=1194 \
    --build-arg server_proto=udp
```

## Start container on 0.0.0.0:1194
```sh
root@host# docker run -t -i -d --privileged --network host --name openvpn openvpn
```

## Setup masquedading for vpn traffic
```sh
root@host# iptables -t nat -A POSTROUTING -s 10.198.199.0/24 -o eth0 -j MASQUERADE
```

## Get OpenVPN client config file
```sh
root@host# docker cp CONTAINER_ID:/etc/openvpn/client.conf ./
```
