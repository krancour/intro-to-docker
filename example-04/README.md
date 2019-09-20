# Compiling as We Build the Image

In the previous example, it inconvenient that we had to pre-compile the binary.
What if we build the executable as a step in building the image? We can!

Modify the `Dockerfile` like so:

```docker
FROM golang:1.12.9

COPY hello-world.go .

RUN go build -o /app/bin/hello-world hello-world.go

CMD ["/app/bin/hello-world"]
```

Rebuild the image:

```console
$ docker build -t go-hello-world:v2 .
```

And run it:

```console
$ docker run go-hello-world:v2
```
