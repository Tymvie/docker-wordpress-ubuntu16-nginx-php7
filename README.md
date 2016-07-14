# docker-wordpress-ubuntu16-nginx-php7

A Dockerfile that installs the latest wordpress on Ubuntu 16.04 with nginx 1.10.0, php-fpm7.0, php7.0 APC User Cache and  openssh. Based heavily on [this](https://hub.docker.com/r/thomasvan/docker-wordpress-ubuntu16-nginx-php7/).

###Todo:

1. If anyone has suggestions please leave a comment on [this GitHub issue](https://github.com/thomasvan/docker-wordpress-ubuntu16-nginx-php7/issues/2).
2. Implement [Docker Compose](https://docs.docker.com/compose/) for a quicker setup.
3. Clean up README.
4. Requests? Just make a comment on [this GitHub issue](https://github.com/thomasvan/docker-wordpress-ubuntu16-nginx-php7/issues/1) if there's anything you'd like added or changed.

## Installation

The easiest way get up and running with this docker container is to pull the latest stable version from the [Docker Hub Registry](https://hub.docker.com/r/thomasvan/docker-wordpress-ubuntu16-nginx-php7/):

```bash
$ docker pull thomasvan/docker-wordpress-ubuntu16-nginx-php7:latest
```

If you'd like to build the image yourself:

```bash
$ git clone https://github.com/thomasvan/docker-wordpress-ubuntu16-nginx-php7.git
$ cd docker-wordpress-nginx-ssh
$ sudo docker build -t="thomasvan/docker-wordpress-ubuntu16-nginx-php7" .
```

## Usage

The -p 80:80 maps the internal docker port 80 to the outside port 80 of the host machine. The other -p sets up sshd on port 2222.

```bash
$ sudo docker run -p 8080:80 -p 2222:22 --name docker-name -d thomasvan/docker-wordpress-ubuntu16-nginx-php7:latest
```

Start your newly created container, named *docker-name*.

```
$ sudo docker start docker-name
```

After starting the container docker-wordpress-nginx-ssh checks to see if it has started and the port mapping is correct.  This will also report the port mapping between the docker container and the host machine.

```
$ sudo docker ps

0.0.0.0:80->80/tcp, 3306/tcp, 0.0.0.0:2222->22/tcp
```

You can then visit the following URL in a browser on your host machine to get started:

```
http://127.0.0.1:8080
```

You can also SSH to your container on 127.0.0.1:2222. The default password is *wordpress*, and can also be found in .ssh-default-pass.

```
$ ssh -p 2222 wordpress@127.0.0.1
# To drop into root
$ sudo -s
```

Now that you've got SSH access, you can setup your FTP client the same way, or the SFTP Sublime Text plugin, for easy access to files.


You can view logs like this:

```
$ sudo docker logs docker-name
```