FROM linuxkit/alpine:35b33c6b03c40e51046c3b053dd131a68a26c37a AS build

RUN apk add --no-cache go musl-dev git build-base
ENV GOPATH=/go PATH=$PATH:/go/bin GO111MODULE=off
ENV COMMIT=db7b7b0f8147f29360d69dc81af9e2877647f0de

RUN git clone https://github.com/moby/vpnkit.git /go/src/github.com/moby/vpnkit && \
    cd /go/src/github.com/moby/vpnkit && \
    git checkout $COMMIT && \
    cd go && \
    make build/vpnkit-iptables-wrapper.linux build/vpnkit-expose-port.linux

FROM scratch
COPY --from=build /go/src/github.com/moby/vpnkit/go/build/vpnkit-iptables-wrapper.linux /usr/bin/vpnkit-iptables-wrapper
COPY --from=build /go/src/github.com/moby/vpnkit/go/build/vpnkit-expose-port.linux /usr/bin/vpnkit-expose-port
