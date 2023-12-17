ARG ALPINE_VERSION=3.19
ARG GO_VERSION=1.21.5
ARG XCPU_VERSION=v0.8.2
ARG BUILDPLATFORM=linux/amd64

FROM --platform=${BUILDPLATFORM} kbuley/xcputranslate:${XCPU_VERSION} AS xcputranslate

FROM --platform=${BUILDPLATFORM} golang:${GO_VERSION}-alpine${ALPINE_VERSION} AS build
ENV CGO_ENABLED=0

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=DL3018
RUN apk add --no-cache git && \
  git config --global advice.detachedHead false
COPY --from=xcputranslate /xcputranslate /usr/local/bin/xcputranslate
WORKDIR /tmp/build

ARG VERSION=v1.21.2
RUN git clone --depth 1 --branch ${VERSION} https://github.com/go-delve/delve.git . && go mod download
ARG TARGETPLATFORM
RUN echo "Building for ${TARGETPLATFORM}..." && \
  if [ "${TARGETPLATFORM}" = "linux/amd64" ] || [ "${TARGETPLATFORM}" = "linux/arm64" ]; then \
  GOARCH="$(xcputranslate translate -field arch -targetplatform ${TARGETPLATFORM})" \
  GOARM="$(xcputranslate translate -field arm -targetplatform ${TARGETPLATFORM})" \
  go build -trimpath -ldflags="-s -w" -o /tmp/bin ./cmd/dlv && \
  chmod 500 /tmp/bin && \
  exit 0; \
  fi && \
  wget -qO- https://raw.githubusercontent.com/kbuley/binpot/main/unavailable/build.sh | \
  sh -s -- "dlv ${VERSION}" "${TARGETPLATFORM}"

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
  org.opencontainers.image.url="https://github.com/kbuley/binpot/blob/main/dockerfiles/dlv" \
  org.opencontainers.image.documentation="https://github.com/kbuley/binpot" \
  org.opencontainers.image.source="https://github.com/kbuley/binpot.git" \
  org.opencontainers.image.title="Dlv binary" \
  org.opencontainers.image.description="Dlv binary"
COPY --from=build /tmp/bin /bin
