# ownCloud , virtualization storage solutions

## Reference

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-owncloud-on-ubuntu-16-04

## What is ownCloud?

ownCloud is a self-hosted file sync and share server. It provides access to your data through a web interface, sync clients or WebDAV while providing a platform to view, sync and share across devices easily—all under your control. ownCloud’s open architecture is extensible via a simple but powerful API for applications and plugins and it works with any storage.

[owncloud.org](https://owncloud.org/)

![alt text](https://raw.githubusercontent.com/docker-library/docs/9d36b4ed7cabc35dbd3849272ba2bd7abe482172/owncloud/logo.png)

## How to build ?

### Prerequisites

* docker

### Build

* change directory to where the Dockerfile is.

* build image use :

```
docker build .
```

or you can specify the file with the other names , and tag the image , see

https://docs.docker.com/engine/reference/builder/

### RUN

use below command to run a container :

```
docker run --name owncloud -p port:80 -itd image
```

## How to visit ?

use url as below to visit :

```
http://ip:port/owncloud
```

## Database

When you visit your ownCloud for the first time , you will be asked for a database to use for it , i recommand you to use docker too :

```
docker pull mysql:5.6
```

or you can specify a version as you like .

and then :

```
docker run --name ownCloud-db -p port:3306 -itd mysql:5.6
```
