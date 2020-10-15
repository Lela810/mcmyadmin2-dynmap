Branch from Linuxserver/mcmyadmin2 for Dynmap

 
 
 
combines minecraft with a web control panel and admin console so can take a little while to start up.

(https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/mcmyadmin-banner.png)]

## Usage

```
 docker create --name=mcmyadmin \
 -v <path to data>:/minecraft \
 -e PGID=<gid> -e PUID=<uid> \
 -p 8080:8080 -p 25565:25565 \
 linuxserver/mcmyadmin2

```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 8080:8080` - Mcmyadmin webui port. 
* `-p 25565:25565` -  Minecraft game server port.
* `-v <path to data>:/minecraft` - The location to store all your permanent files server jars\maps\configs and more.
* `-e PGID` numeric GroupID - see below for explanation
* `-e PUID` numeric UserID - see below for explanation

It is based on ubuntu xenial with s6 overlay, for shell access whilst the container is running do `docker exec -it mcmyadmin /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application

**Minimum of 2GB of ram required for this container to work properly.**

After starting the container, log into the Web UI as the `admin` user with the password `password` and change the password.
You should also consider serving the admin UI over https.

To add the Dynmap extension (Lela810/McMyAdmin-Dynmapextension) to your MCMA move the Dynmap Folder to /minecraft/Modern/Extensions.
Dynmap default Port: 8123
