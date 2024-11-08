---
title:  "Running the Duo Auth Proxy in Docker"
categories: [Duo,Docker]
---

# Running the Duo Auth Proxy in Docker
Why? Cause I'm a monster. 

This is based on the details and steps in https://registry.hub.docker.com/r/minimages/duoauthproxy and is working running on a Synology NAS and deployed by portainer. 

The ports are to allow RADIUS, LDAP and LDAP connections to the Duo Authentication Proxy. 
The logs and config file are stored on external volumes so aren't overwritten by any upgrates. 

```
services:
  duoauthproxy:
    image: minimages/duoauthproxy
    ports:
        - "1812:1812"
        - "389:389"
        - "636:636"
    volumes:
        - /volume1/docker/duoauthproxy/authproxy.cfg:/app/conf/authproxy.cfg
        - /volume1/docker/duoauthproxy/log:/app/log
    restart: unless-stopped
```