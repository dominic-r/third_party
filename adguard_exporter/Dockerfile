FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c AS certs
RUN apk add ca-certificates

FROM golang:1.24.3@sha256:4c0a1814a7c6c65ece28b3bfea14ee3cf83b5e80b81418453f0e9d5255a5d7b8 AS builder
WORKDIR /build
COPY . /build
RUN go mod download
RUN CGO_ENABLED=0 go build -a -o adguard-exporter main.go

FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c

COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /build/adguard-exporter /adguard-exporter

USER 65532:65532
ENTRYPOINT ["/adguard-exporter"]
