# Dockerfile

FROM alpine:3.3
MAINTAINER @pottava

LABEL com.github.pottava.application="docker-webui" \
      com.github.pottava.description="A web user-interface for docker." \
      com.github.pottava.usage="docker run -d -p 80:9000 -e DOCKER_HOST=unix:///var/run/docker.sock  -v /var/run/docker.sock:/var/run/docker.sock pottava/docker-webui" \
      com.github.pottava.license="MIT"

ENV GOPATH=/go PATH=/go/bin:$PATH

RUN apk --no-cache add --virtual build-dependencies go git \
      && mkdir -p /go/src /go/bin \
      && chmod -R 777 /go \
      && go get -u github.com/pottava/docker-webui \
      && apk del --purge build-dependencies \
      && rm -rf /go/pkg \
          /go/src/golang.org \
          /go/src/github.com/fsouza \
          /go/src/github.com/pottava/docker-webui/.git* \
          /go/src/github.com/pottava/docker-webui/[^a]* \
          /go/src/github.com/pottava/docker-webui/app/[^av]* \
          /go/src/github.com/pottava/docker-webui/app/assets/scss \
          /go/src/github.com/pottava/docker-webui/app/assets/js/clients \
          /go/src/github.com/pottava/docker-webui/app/assets/js/containers \
          /go/src/github.com/pottava/docker-webui/app/assets/js/images

VOLUME ["/var/run/docker.sock"]
EXPOSE 9000

ENTRYPOINT ["/go/bin/docker-webui"]
