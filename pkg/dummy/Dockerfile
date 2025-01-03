FROM linuxkit/alpine:d7d54c626d8c9bee72f31c2781c47b43811a26eb AS build
RUN apk add --no-cache --initdb make

FROM scratch
ENTRYPOINT []
CMD []
WORKDIR /
COPY --from=build /usr/bin/make /usr/bin/
COPY infile infile
