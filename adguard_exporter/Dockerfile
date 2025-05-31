FROM alpine:3.22.0@sha256:8a1f59ffb675680d47db6337b49d22281a139e9d709335b492be023728e11715 AS certs
RUN apk add ca-certificates

FROM golang:1.24.3@sha256:4c0a1814a7c6c65ece28b3bfea14ee3cf83b5e80b81418453f0e9d5255a5d7b8 AS builder
WORKDIR /build
COPY . /build
RUN go mod download
RUN CGO_ENABLED=0 go build -a -o adguard-exporter main.go

FROM alpine:3.22.0@sha256:8a1f59ffb675680d47db6337b49d22281a139e9d709335b492be023728e11715

COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /build/adguard-exporter /adguard-exporter

USER 65532:65532
ENTRYPOINT ["/adguard-exporter"]
