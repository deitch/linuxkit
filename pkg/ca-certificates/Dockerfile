FROM linuxkit/alpine:d7d54c626d8c9bee72f31c2781c47b43811a26eb as alpine

RUN apk add ca-certificates

FROM scratch
ENTRYPOINT []
WORKDIR /
COPY --from=alpine /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
