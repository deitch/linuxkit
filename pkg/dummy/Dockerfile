FROM linuxkit/alpine:90c717aa6b59afa0c3c69623ee7f74d3da8d9316 AS build
RUN apk add --no-cache --initdb make

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=build /usr/bin/make /usr/bin/
COPY infile infile
