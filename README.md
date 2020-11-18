# docker-ikev2-vpn
Dockerized IKEv2 VPN server

## Build
    $ cd docker-ikev2-vpn

    $ docker build -t zms-nemoto/ikev2-vpn .

## Usage
    $ docker run \
        --restart=always \
        --detach \
        --privileged \
        --sysctl net.ipv4.ip_forward=1 \
        --sysctl net.ipv4.conf.all.accept_redirects=0 \
        --sysctl net.ipv4.conf.all.send_redirects=0 \
        --sysctl net.ipv4.ip_no_pmtu_disc=1 \
        --volume=/lib/modules:/lib/modules \
        --volume=/opt/vpn-setting/ipsec.d:/etc/ipsec.d \
        --publish=500:500/udp \
        --publish=4500:4500/udp \
        --env NAME="<VPN Server Name>" \
        --env HOST="<Host IP>" \
        --name=ikev2-vpn \
        zms-nemoto/ikev2-vpn


### To view and download the certificate:

    $ docker exec ikev2-vpn manage certificate


### To add a user:

    $ docker exec ikev2-vpn manage adduser <username> <password>
