FROM golang:1.12.1-alpine AS builder
WORKDIR $GOPATH/src/github.com/nats-io/nats-streaming-operator/
COPY . .
RUN apk add --update git
RUN CGO_ENABLED=0 GO111MODULE=on GOARCH=arm GOARM=7 go build -installsuffix cgo -o /nats-streaming-operator ./cmd/nats-streaming-operator/main.go

FROM arm32v7/alpine:3.10.3
COPY --from=builder /nats-streaming-operator /usr/local/bin/nats-streaming-operator
CMD ["nats-streaming-operator"]
