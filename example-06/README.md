# Lightweight Distributions

But we can do better!

What if we base our final image on a smaller, more lightweight Linux
distribution, such as Alpine?

Modify the `Dockerfile` like so:

```docker
FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM alpine:3.10.2
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
```

Build it:

```console
$ docker build -t go-hello-world:v4 .
```

And run it:

```console
$ docker run go-hello-world:v4
```

And we can see this image is smaller than any other one we've built so far-- by
a wide margin:

```console
$ docker images | grep go-hello-world
go-hello-world                       v4                  5c2519be64ed        About a minute ago   7.59MB
go-hello-world                       v3                  325a29162d88        4 minutes ago        116MB
go-hello-world                       v2                  408ad1e146b7        36 minutes ago       805MB
go-hello-world                       v1                  c9a91410869c        43 minutes ago       116MB
```
