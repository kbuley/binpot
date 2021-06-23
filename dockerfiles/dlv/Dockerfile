ARG ALPINE_VERSION=3.13
ARG GO_VERSION=1.16
ARG XCPU_VERSION=v0.6.0
ARG BUILDPLATFORM=linux/amd64

FROM --platform=${BUILDPLATFORM} qmcgaw/xcputranslate:${XCPU_VERSION} AS xcputranslate

FROM --platform=${BUILDPLATFORM} golang:${GO_VERSION}-alpine${ALPINE_VERSION} AS build
ENV CGO_ENABLED=0
RUN apk add --no-cache git && \
    git config --global advice.detachedHead false
COPY --from=xcputranslate /xcputranslate /usr/local/bin/xcputranslate
WORKDIR /tmp/build

ARG VERSION=v1.6.1
RUN git clone --depth 1 --branch ${VERSION} https://github.com/go-delve/delve.git .
RUN go mod download
ARG TARGETPLATFORM
RUN export GOARCH="$(xcputranslate translate -field arch -targetplatform ${TARGETPLATFORM})" && \
    export GOARM="$(xcputranslate translate -field arm -targetplatform ${TARGETPLATFORM})" && \
    if [ "${TARGETPLATFORM}" = "linux/amd64" ] || [ "${TARGETPLATFORM}" = "linux/arm64" ]; then \
        echo "Building for ${TARGETPLATFORM}..." && \
        COMMIT="$(git rev-parse --short HEAD)" && \
        DATE="$(date +%Y-%m-%dT%T%z)" && \
        go build -trimpath -ldflags="-s -w" -o /tmp/bin ./cmd/dlv && \
        chmod 500 /tmp/bin && \
        exit 0; \
    fi && \
    wget -qO- https://raw.githubusercontent.com/qdm12/binpot/main/unavailable/build.sh | \
       sh -s -- "dlv ${VERSION}" "${TARGETPLATFORM}"

FROM scratch
ENTRYPOINT [ "/bin" ]
ARG VERSION
ARG CREATED
ARG REVISION
LABEL \
    org.opencontainers.image.authors="quentin.mcgaw@gmail.com" \
    org.opencontainers.image.version=${VERSION} \
    org.opencontainers.image.created=${CREATED} \
    org.opencontainers.image.revision=${REVISION} \
    org.opencontainers.image.url="https://github.com/qdm12/binpot/blob/main/dockerfiles/dlv" \
    org.opencontainers.image.documentation="https://github.com/qdm12/binpot" \
    org.opencontainers.image.source="https://github.com/qdm12/binpot.git" \
    org.opencontainers.image.title="Dlv binary" \
    org.opencontainers.image.description="Dlv binary"
COPY --from=build /tmp/bin /bin