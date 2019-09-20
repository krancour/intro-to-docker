FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM debian:10.1
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
