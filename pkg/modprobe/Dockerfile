# Dockerfile to build linuxkit/modprobe for linuxkit
FROM linuxkit/alpine:90c717aa6b59afa0c3c69623ee7f74d3da8d9316 AS mirror

RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    busybox
RUN rm -rf /out/var/cache

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=mirror /out/ /
