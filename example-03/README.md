## Creating Our First Image

Images are defined using a `Dockerfile`. A `Dockerfile` is a set of instructions
for constructing a new image by starting with a "base image" and then layering
in other packages, files, and configuration.

In this example, we'll create our own hello-world program using Go, compile it,
and add the executable to our image. (If you don't have a Go compiler installed
on your system, hang in there. The next example will suit you better!)

Create and save `hello-world.go` with the following contents:

```golang
package main

import "fmt"

func main() {
  fmt.Println("Hello, World!")
}
```

Cross-compile it for `linux/amd64`:

```console
$ GOOS=linux GOARCH=amd64 go build -o bin/hello-world hello-world.go
```

Create and save __Dockerfile__ with the following contents:

```docker
FROM debian:10.1

COPY bin/hello-world /app/bin/hello-world

CMD ["/app/bin/hello-world"]
```

This starts with Debian linux, layers in the binary we built, and sets it as the
default process for containers based on this image.

We can now build this, "tagging" the image with a convenient name as we do:

```console
$ docker build -t go-hello-world:v1 .
```

And we can run a container based on the resulting image:

```console
$ docker run go-hello-world:v1
```