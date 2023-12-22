# syntax=docker/dockerfile:1
ARG ALPINE_VERSION=3.19
ARG GO_VERSION=1.21.5
ARG XCPU_VERSION=v0.8.2
ARG BUILDPLATFORM=linux/amd64

ARG BUILDX_VERSION=0.11.2
FROM docker/buildx-bin:${BUILDX_VERSION} AS buildx

FROM golang:${GO_VERSION}-alpine${ALPINE_VERSION} AS golang
ENV GOTOOLCHAIN=local
ENV CGO_ENABLED=0

FROM golang AS gofumpt
ARG GOFUMPT_VERSION=v0.4.0
RUN --mount=type=cache,target=/root/.cache/go-build \
  --mount=type=cache,target=/go/pkg/mod \
  --mount=type=tmpfs,target=/go/src/ \
  GO111MODULE=on go install "mvdan.cc/gofumpt@${GOFUMPT_VERSION}" \
  && gofumpt --version

FROM golang AS gotestsum
ARG GOTESTSUM_VERSION=v1.10.0
RUN --mount=type=cache,target=/root/.cache/go-build \
  --mount=type=cache,target=/go/pkg/mod \
  --mount=type=tmpfs,target=/go/src/ \
  GO111MODULE=on go install gotest.tools/gotestsum@${GOTESTSUM_VERSION}

FROM golang AS goversioninfo
ARG GOVERSIONINFO_VERSION=v1.3.0
RUN --mount=type=cache,target=/root/.cache/go-build \
  --mount=type=cache,target=/go/pkg/mod \
  --mount=type=tmpfs,target=/go/src/ \
  GO111MODULE=on go install github.com/josephspurrier/goversioninfo/cmd/goversioninfo@${GOVERSIONINFO_VERSION}

FROM golang AS dev
ARG DOCKER_VERSION=v24.0.7
# hadolint ignore=DL3018
RUN  apk add --no-cache bash build-base ca-certificates coreutils curl git jq

CMD ["bash", "-c"]
ENV DISABLE_WARN_OUTSIDE_CONTAINER=1
ENV PATH=$PATH:/go/src/github.com/docker/cli/build

COPY --link --from=buildx          /buildx /usr/libexec/docker/cli-plugins/docker-buildx
COPY --link --from=gofumpt         /go/bin/* /go/bin/
COPY --link --from=gotestsum       /go/bin/* /go/bin/
COPY --link --from=goversioninfo   /go/bin/* /go/bin/

WORKDIR /go/src/github.com/docker/cli
ENV GO111MODULE=auto

RUN git clone --depth 1 --branch ${DOCKER_VERSION} https://github.com/docker/cli . && \
  make binary && \
  cp build/docker /tmp/bin && \
  chmod +x /tmp/bin

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
  org.opencontainers.image.url="https://github.com/kbuley/binpot/blob/main/dockerfiles/docker" \
  org.opencontainers.image.documentation="https://github.com/kbuley/binpot" \
  org.opencontainers.image.source="https://github.com/kbuley/binpot.git" \
  org.opencontainers.image.title="Docker binary" \
  org.opencontainers.image.description="Docker binary"
COPY --from=dev /tmp/bin /bin
