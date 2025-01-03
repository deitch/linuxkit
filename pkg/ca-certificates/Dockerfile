FROM linuxkit/alpine:90c717aa6b59afa0c3c69623ee7f74d3da8d9316 as alpine

RUN apk add ca-certificates

FROM scratch
ENTRYPOINT []
WORKDIR /
COPY --from=alpine /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
