ARG ALPINE_VERSION=3.19
ARG GO_VERSION=1.21.5
ARG XCPU_VERSION=v0.8.2
ARG BUILDPLATFORM=linux/amd64

FROM --platform=${BUILDPLATFORM} kbuley/xcputranslate:${XCPU_VERSION} AS xcputranslate

FROM --platform=${BUILDPLATFORM} golang:${GO_VERSION}-alpine${ALPINE_VERSION} AS build
ENV CGO_ENABLED=0

# hadolint ignore=DL3018
RUN apk add --no-cache git && \
  git config --global advice.detachedHead false
COPY --from=xcputranslate /xcputranslate /usr/local/bin/xcputranslate
WORKDIR /tmp/build

ARG VERSION=v0.40.2
RUN git clone --depth 1 --branch ${VERSION} https://github.com/jesseduffield/lazygit.git . && go mod download
ARG TARGETPLATFORM
RUN echo "Building for ${TARGETPLATFORM}..." && \
  GOARCH="$(xcputranslate translate -field arch -targetplatform ${TARGETPLATFORM})" \
  GOARM="$(xcputranslate translate -field arm -targetplatform ${TARGETPLATFORM})" \
  go build -trimpath -ldflags="-s -w \
  -X 'main.version=${VERSION}' \
  -X 'main.commit=$(git rev-parse --short HEAD)' \
  -X 'main.date=$(date)' \
  -X 'main.buildSource=github' \
  " -o /tmp/bin ./cmd/lazygit && \
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
  org.opencontainers.image.url="https://github.com/kbuley/binpot/blob/main/dockerfiles/lazygit" \
  org.opencontainers.image.documentation="https://github.com/kbuley/binpot" \
  org.opencontainers.image.source="https://github.com/kbuley/binpot.git" \
  org.opencontainers.image.title="lazygit binary" \
  org.opencontainers.image.description="lazygit binary"
COPY --from=build /tmp/bin /bin
