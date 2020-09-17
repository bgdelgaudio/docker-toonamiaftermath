 
## [th3bluecarp/docker-toonamiaftermath](https://github.com/th3bluecarp/docker-toonamiaftermath)

[![https://www.toonamiaftermath.com/](https://vignette.wikia.nocookie.net/toonami/images/0/0f/Toonami_aftermath_logo.png/revision/latest?cb=20121120205018)](https://www.toonamiaftermath.com/)

This is a fork of [chris102994](https://github.com/chris102994/docker-toonamiaftermath)'s original creation with the intent of adding additional streams from the site as well as pushing to Docker Hub for easier Unraid integration.

[Toonami Aftermath](https://www.toonamiaftermath.com/) is a Toonami revival effort, which began as a 24/7 stream, launched on January 18, 2010 with its website appearing a few months after that. It airs programs that have been broadcast on Toonami, and also Cartoon Network, Fox, and Kids WB, such as Ronin Warriors, Cartoon Cartoons, X-Men: The Animated Series, and Pokemon. 

I do not officially endorse the Toonami Aftermath project or its affiliates. 

This is a simple project that scrapes the website and generates an m3u playlist along with a XmlTV that can be managed with [xteve](https://xteve.de/) so that live tv players such as Emby or Plex can view the channels. 


## Outside Packages
* Built on chris102994's [xteve Image](https://github.com/chris102994/docker-xteve)

## Docker
```
docker run \
	--name=docker-toonamiaftermath \
	-p 34400:34400 \
	-v </path/to/appdata/config>:/config `optional if you dont plan to modify the xteve config` \
  	-e NUMBER_OF_STREAMS=1 `optional` \
  	-e STREAM_BUFFER=ffmpeg `optional` \
  	-e XTEVE_PORT=34400 `optional unless you change the port mapping` \
	--restart unless-stopped \
	christopher102994/docker-toonamiaftermath:alpine-3.10
```

## Parameters
Container specific parameters passed at runtime. The format is `<external>:<internal>` (e.g. `-p 443:22` maps the container's port 22 to the host's port 443).

| Parameter | Function |
| -------- | -------- |
| -p 34400 | This is the port inside the container by default however, you should map the outside port to be the same as the inner port and set the `XTEVE_PORT` environment variable to also match. (Default=34400) |
| -v /config | The directory where the application will store configuration information. |
| -e NUMBER_OF_STREAMS | Number of parallel connections that the container will re-stream. (Default=1) |
| -e STREAM_BUFFER | What the container uses to re-stream. Options: '-'=none (Default), 'xteve'=xteve, 'ffmpeg' , 'vlc' |
| -e XTEVE_PORT | This must match the port you map to the container so that xteve can correctly forward the stream. (Default=34400) |
| -e USERNAME | The Username you wish to run as. (Optional) |
| -e GROUPNAME | The Groupname you wish to run as. (Optional) |
| -e PUID | The UID you wish to run and save files as. (Optional) |
| -e PGID | The GID you wish to run and save files as. (Optional) |

## Application Setup

Note: if currently running an instance of xTeve, port needs to be changed to something other than '34400'.

The admin interface is available at `http://<ip>:<port>/web/`

This will build and allow you to point your M3U Tuner to `http://<ip>:<port>/m3u/xteve.m3u`
and your XEPG tuner to `http://<ip>:port/xmltv/xteve.xml`
