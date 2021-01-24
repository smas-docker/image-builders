### Dockerfile
#
#   See https://github.com/russmckendrick/docker

FROM alpine:latest

LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL org.opencontainers.image.source https://github.com/atv-docker/image-builders
LABEL org.opencontainers.image.description "A base image, useful for starting container builds, see this containers GitHub repo for more info"

RUN apk update && apk upgrade && \
	apk add ca-certificates bash && \
	rm -rf /var/cache/apk/*
