## Build stage
FROM golang:1.17-bullseye as build
WORKDIR /go/src/app
COPY ./src/ /go/src/app

RUN go get -d -v ./... && \
    go build -o /go/bin/app


## Development evironment
FROM golang:1.17-bullseye as development
WORKDIR /
EXPOSE 8000/tcp
COPY --from=build /go/src/app/web /web/
COPY --from=build /go/bin/app /
CMD ["/app"]

## Distroless
FROM gcr.io/distroless/base-debian11 as production
WORKDIR /
EXPOSE 8000/tcp
COPY --from=build /go/src/app/web /web/
COPY --from=build /go/bin/app /
CMD ["/app"]

