# Host System
Install [Ubuntu](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview) with [Docker](https://docs.docker.com/engine/install/ubuntu/) and build the Docker-Image.


# build the image
```cd``` into the traget dir.

```
# base image
cd base
docker build --tag paco:base .
cd -

# ui image
cd ui
docker build --tag paco:ui .
cd -
```

# start the container
```
# DANGER: if you set ip 0.0.0.0 the container can be accessed without password in the local network.
docker run -d -p 127.0.0.1:40001:40001 -p 127.0.0.1:5901:5901 --name=paco --privileged paco:ui
```

# access container
[localhost:40001](localhost:40001)
* username: ```syslab```
* password: ```syslab```
