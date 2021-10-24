FROM golang:1-alpine AS build-env

ARG VERSION=""

COPY . /project

RUN set -xe \
    && cd /project/cmd/hello-service \
    && go mod download \
    && CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-w -s -X main.version=${VERSION}" -o hello-service

FROM scratch

COPY --from=build-env /project/cmd/hello-service/hello-service /app/

EXPOSE 8000

ENTRYPOINT ["/app/hello-service"]
