ARG ALPINE_VERSION=3.19
ARG XCPU_VERSION=v0.8.2
ARG BUILDPLATFORM=linux/amd64

FROM --platform=${BUILDPLATFORM} kbuley/xcputranslate:${XCPU_VERSION} AS xcputranslate
FROM --platform=${BUILDPLATFORM} alpine:${ALPINE_VERSION} AS build

# hadolint ignore=DL3018
RUN apk add --no-cache wget g++ make binutils cmake git && \
  git config --global advice.detachedHead false && \
  apk add --no-cache -X "https://dl-cdn.alpinelinux.org/alpine/v3.14/community" gcc-cross-embedded
COPY --from=xcputranslate /xcputranslate /usr/local/bin/xcputranslate
WORKDIR /tmp/build

ARG VERSION=v1.5.4

# hadolint ignore=DL3018
RUN git clone --depth 1 --branch ${VERSION} https://github.com/romkatv/gitstatus.git . && \
  apk add --no-cache --update -X "https://dl-cdn.alpinelinux.org/alpine/v3.14/community" gcc-cross-embedded
ARG TARGETPLATFORM
RUN echo "Building for ${TARGETPLATFORM}..." && \
  UNAMEM="$(xcputranslate translate -language uname -targetplatform ${TARGETPLATFORM})" && \
  ./build -w -m "${UNAMEM}" && \
  mv ./usrbin/gitstatusd /tmp/bin && \
  chmod 500 /tmp/bin

FROM scratch
ENTRYPOINT [ "/bin" ]
ARG VERSION
ARG CREATED
ARG REVISION
LABEL \
  org.opencontainers.image.authors="kevin@buley.org" \
  org.opencontainers.image.version=${VERSION} \
  org.opencontainers.image.created=${CREATED} \
  org.opencontainers.image.revision=${REVISION} \
  org.opencontainers.image.url="https://github.com/kbuley/binpot/blob/main/dockerfiles/gotests" \
  org.opencontainers.image.documentation="https://github.com/kbuley/binpot" \
  org.opencontainers.image.source="https://github.com/kbuley/binpot.git" \
  org.opencontainers.image.title="Gitstatusd binary" \
  org.opencontainers.image.description="Gitstatusd binary"
COPY --from=build /tmp/bin /bin
