# Running Something Less Trivial

How about running a web server using an existing image? This time, we'll bind a
host port to the port that the web server is listening to inside the container.
This will permit us to communicate with the web server from outside the
container.

```console
$ docker run -p 8080:80 nginx:1.17.3
```

In a separate terminal:

```console
$ open http://localhost:8080
```

Back in the first terminal, use `ctrl + C` to interrupt the Nginx process in the
container. Alternatively, use another terminal to identify and kill the
container.

```console
$ docker ps
$ docker kill <container id or name>
```
