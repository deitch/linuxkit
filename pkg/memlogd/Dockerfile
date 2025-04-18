# Dockerfile to build linuxkit/memlogd for linuxkit
FROM linuxkit/alpine:35b33c6b03c40e51046c3b053dd131a68a26c37a AS build

RUN apk add --no-cache go musl-dev
ARG GOPKGVERSION
ENV ldflags="-X main.Version=$GOPKGVERSION"
ENV GOPATH=/go PATH=$PATH:/go/bin
# Hack to work around an issue with go on arm64 requiring gcc
RUN [ $(uname -m) = aarch64 ] && apk add --no-cache gcc || true

COPY . /go/src/memlogd
RUN go-compile.sh /go/src/memlogd/cmd/memlogd
RUN go-compile.sh /go/src/memlogd/cmd/logread
RUN go-compile.sh /go/src/memlogd/cmd/logwrite

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=build /go/bin/memlogd usr/bin/memlogd
COPY --from=build /go/bin/logread usr/bin/logread
COPY --from=build /go/bin/logwrite usr/bin/logwrite
# We'll start from init.d
COPY etc/ /etc/
COPY --from=build /etc/apk /etc/apk/
COPY --from=build /lib/apk /lib/apk/
