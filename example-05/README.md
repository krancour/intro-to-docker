# Multi-Stage Builds

Our previous example produced a somewhat bloated image. We only needed Go to
_compile_ our program, but do not require it to run it.

Let's list images to see how big our first two images were:

```console
$ docker images | grep go-hello-world
go-hello-world                       v2                  408ad1e146b7        11 minutes ago      805MB
go-hello-world                       v1                  c9a91410869c        18 minutes ago      116MB
```

Clearly, this level of bloat is unacceptable.

Fortunately, we can use _multi-stage_ builds to use one container as a utility
for building our binary, then package that binary into a separate, smaller
image:

Modify the `Dockerfile` like so:

```docker
FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM debian:10.1
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
```

Build it:

```console
$ docker build -t go-hello-world:v3 .
```

And run it:

```console
$ docker run go-hello-world:v3
```

And we can see this image is smaller than our previous one:

```console
$ docker images | grep go-hello-world
go-hello-world                       v3                  325a29162d88        22 seconds ago      116MB
go-hello-world                       v2                  408ad1e146b7        32 minutes ago      805MB
go-hello-world                       v1                  c9a91410869c        39 minutes ago      116MB
```
