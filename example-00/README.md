# Dipping Our Toes In

How fast can you start an Ubuntu VM and get to a bash prompt? Probably not
faster than I can start an Ubuntu container:

```console
$ docker run -it ubuntu:18.04 bash
```

The `docker run` command launches a container. The `-i` and `-t` options
(shortened to `-it`) attach an interative terminal to the container.
`ubuntu:18.04` is the image on which we'll base our container. `bash` is the
process we wish to execute within the container.

The first time you run this command, Docker will automatically fetch the
`ubuntu:18.04` image from the Docker Hub repository since it does not already
exist on your system.

We can explore this container. Let's look at who we are and what processes are
running.

```console
$ whoami
root
$ ps guax
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  18504  3460 pts/0    Ss   20:27   0:00 bash
root        14  0.0  0.1  34396  2816 pts/0    R+   20:29   0:00 ps guax
```

We can install packages using the `apt-get` package manager:

```console
$ apt-get update
$ apt-get install -y curl
```

And use the newly installed software:

```console
$ curl https://www.npr.org
```

In a separate terminal, we can see this container is running:

```console
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
44257553433a        ubuntu:18.04        "bash"              5 minutes ago       Up 5 minutes                            fervent_heyrovsky
```

Back in our first terminal, we can exit the `bash` process, which will prompt
the container to stop as well. All changes we made to the container were
ephemeral. They are gone. If we launch a new container, we get a fresh start.

There are other ways to kill a running container. First start a new one:

```console
$ docker run -it ubuntu:18.04 bash
```

And then, in another terminal:

```console
$ docker ps
$ docker kill <container id or name>
```
