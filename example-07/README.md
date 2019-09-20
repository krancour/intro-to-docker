# Scratch Images

Believe it or not, we can do better still. Our hello-world application doesn't
require, really, anything other than the binary and the Linux kernel. We can
base our final image on `scratch`-- an empty image.

Modify the `Dockerfile` like so:

```docker
FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM scratch
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
```

Build it:

```console
$ docker build -t go-hello-world:v5 .
```

And run it:

```console
$ docker run go-hello-world:v5
```

Looking at image sizes, once again, we find that our latest iteration is a mere
2.01 MB!

```console
$ docker images | grep go-hello-world
go-hello-world                       v5                  3bbc44e1fe09        10 seconds ago      2.01MB
go-hello-world                       v4                  5c2519be64ed        5 minutes ago       7.59MB
go-hello-world                       v3                  325a29162d88        8 minutes ago       116MB
go-hello-world                       v2                  408ad1e146b7        40 minutes ago      805MB
go-hello-world                       v1                  c9a91410869c        47 minutes ago      116MB
```
