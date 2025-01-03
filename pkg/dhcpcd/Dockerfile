FROM linuxkit/alpine:d7d54c626d8c9bee72f31c2781c47b43811a26eb AS mirror
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
