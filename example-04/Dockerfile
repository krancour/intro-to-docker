FROM golang:1.12.9

COPY hello-world.go .

RUN go build -o /app/bin/hello-world hello-world.go

CMD ["/app/bin/hello-world"]
