# OpenVpn minimal docker image

[![Build Status](https://travis-ci.org/bertrandmartel/docker-openvpn.svg?branch=master)](https://travis-ci.org/bertrandmartel/docker-openvpn)
[![](https://images.microbadger.com/badges/version/bertrandmartel/docker-openvpn.svg)](http://microbadger.com/images/bertrandmartel/docker-openvpn)
[![](https://images.microbadger.com/badges/image/bertrandmartel/docker-openvpn.svg)](http://microbadger.com/images/bertrandmartel/docker-openvpn)

A minimal OpenVpn docker image to be run with an already existing configuration

Place your configuraton `/etc/openvpn` directory in a local `config` directory. This configuration directory should contain `openvpn.conf` for your server/client configuration file

## Build image

```
docker build -t openvpn .
```

## Usage

* store path to your configuration folder : 

```
VPN_CONFIG="config"
```

* start openvpn  :

```
docker run -v $VPN_CONFIG:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN bertrandmartel/docker-openvpn
```

## Docker-compose

```
docker-compose up
```

## Docker-cloud

```
export USER_PATH=/home/bobby
envsubst < stackfile-template.yml > stackfile.yml
```

* revise your `stackfile.yml` file before creating/updating the stack :

```
# create the stack :

docker-cloud stack create --name openvpn -f stackfile.yml

# or update :

docker-cloud stack update -f stackfile.yml <uuid>
```

* start/deploy :

```
# start the stack :

docker-cloud stack start <uuid>

# or redeploy :

docker-cloud stack redeploy <uuid>
```

## Debug 

```
docker exec -it openvpn  bash
```