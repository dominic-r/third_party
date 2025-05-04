FROM --platform=$BUILDPLATFORM docker.io/library/golang:1.24.2-bookworm@sha256:79390b5e5af9ee6e7b1173ee3eac7fadf6751a545297672916b59bfa0ecf6f71 AS build

WORKDIR /go/src/app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY *.go .

ENV CGO_ENABLED=0

RUN GOOS=$TARGETOS GOARCH=$TARGETPLATFORM go build -v -o /go/bin/unbound_exporter ./...

FROM gcr.io/distroless/static-debian12

COPY --from=build /go/bin/unbound_exporter /

ENTRYPOINT ["/unbound_exporter"]