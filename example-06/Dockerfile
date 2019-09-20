FROM golang:1.12.9
COPY hello-world.go .
RUN go build -o /app/bin/hello-world hello-world.go

FROM alpine:3.10.2
COPY --from=0 /app/bin/hello-world /app/bin/hello-world
CMD ["/app/bin/hello-world"]
