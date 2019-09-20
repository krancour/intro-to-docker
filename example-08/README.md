# Using Environment Variables

Let's also explore something useful like setting values for environment
variables either in our `Dockerfile` or at runtime:

Modify `hello-world.go` like so to utilize an environment variable:

```golang
package main

import (
  "fmt"
  "os"
)

func main() {
  name := os.Getenv("NAME")
  if name == "" {
    name = "World"
  }
  fmt.Printf("Hello, %s!\n", name)
}
```

Modify the `Dockerfile` like so:

```docker
FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM scratch
ENV NAME=Docker
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
```

Build it:

```console
$ docker build -t go-hello-world:v6 .
```

And run it:

```console
$ docker run go-hello-world:v6
```

Now let's try overriding this environment variable at runtime!

```console
$ docker run -e NAME=Kent go-hello-world:v6
```
