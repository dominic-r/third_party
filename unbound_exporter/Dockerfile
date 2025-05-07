FROM --platform=$BUILDPLATFORM docker.io/library/golang:1.24.3-bookworm@sha256:89a04cc2e2fbafef82d4a45523d4d4ae4ecaf11a197689036df35fef3bde444a AS build

WORKDIR /go/src/app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY *.go .

ENV CGO_ENABLED=0

RUN GOOS=$TARGETOS GOARCH=$TARGETPLATFORM go build -v -o /go/bin/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12@sha256:3d0f463de06b7ddff27684ec3bfd0b54a425149d0f8685308b1fdf297b0265e9

COPY --from=build /go/bin/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]