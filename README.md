# hongkongkiwi/docker-shadowsocks-client
![](https://images.microbadger.com/badges/version/hongkongkiwi/docker-shadowsocks-libev-client.svg)
![](https://images.microbadger.com/badges/image/hongkongkiwi/docker-shadowsocks-libev-client.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/hongkongkiwi/shadowsocks-libev-client.svg)
![Docker Stars](https://img.shields.io/docker/stars/hongkongkiwi/shadowsocks-libev-client.svg)

Shadowsocks-libev is a lightweight secured SOCKS5 proxy for embedded devices and low-end boxes.

It is a port of Shadowsocks created by @clowwindy, and maintained by @madeye and @linusyang.

Shadowsocks-libev is written in pure C and depends on libev. It's designed to be a lightweight implementation of shadowsocks protocol, in order to keep the resource usage as low as possible.

For a full list of feature comparison between different versions of shadowsocks, refer to the Wiki page.

[![shadowsocks-libev logo](https://gaukas.wang/wp-content/uploads/2015/11/Shadowsocks.png)](https://github.com/shadowsocks/shadowsocks-libev)

## Usage

```
docker create \
--name="shadowsocks-libev-client" \
-v <path to config file>:/config/ss_config.json \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 1080:1080 \
hongkongkiwi/shadowsocks-libev-client
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 1080:1090 would expose port 1080 from inside the container to be accessible from the host's IP on port 1090
http://192.168.x.x:1090 would show you what's running INSIDE the container on port 1080.`


* `-p 1080` - the port(s)
* `-v /config/ss_config.json` - location of configuration file
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for setting timezone information, eg Europe/London

It is based on a minimal alpine linux build, for shell access whilst the container is running do `docker exec -it "shadowsocks-libev-client" /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application

Basic settings are pre-set by this container.  You can use the out of box experience or customize to your own preferences.


## Info

* To monitor the logs of the container in realtime `docker logs -f "shadowsocks-libev-client"`.

## Versions

+ **16.06.17:** Initial Release
