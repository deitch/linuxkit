FROM linuxkit/alpine:90c717aa6b59afa0c3c69623ee7f74d3da8d9316 AS mirror
RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    alpine-baselayout \
    busybox \
    dhcpcd \
    musl

# Remove apk residuals
RUN rm -rf /out/etc/apk /out/lib/apk /out/var/cache

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=mirror /out/ /
# put the config file in / because we bind mount /etc to handle resolv.conf symlinks
COPY /dhcpcd.conf /
COPY /usr/ /usr/
CMD ["/sbin/dhcpcd", "--nobackground", "-f", "/dhcpcd.conf"]
