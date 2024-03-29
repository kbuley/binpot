# Binpot

The statically compiled, cross architecture, Docker based, binaries pot.

<img height="150" src="https://raw.githubusercontent.com/kbuley/binpot/main/binpot.svg">

[Blog post](https://qqq.ninja/blog/post/binpot/)

[![MIT](https://img.shields.io/github/license/kbuley/binpot)](https://github.com/kbuley/binpot/main/LICENSE)

## Usage

The usage is focused to build other Docker images.

For example:

```Dockerfile
FROM alpine:3.14
COPY --from=kbuley/binpot:helm /bin /usr/local/bin/helm
```

[🔍 Search for all image tags 💡](https://hub.docker.com/r/kbuley/binpot/tags)

- The Docker image tags for `kbuley/binpot` follow the following formatting:
  - `:name` for the latest stable version of the program `name`
  - `:name-v0.0.0` for the semver version of the program `name`
- Each Docker image is based on [scratch](https://hub.docker.com/_/scratch) and only contain the binary program at the path `/bin`.
- Each Docker image and binary program is built for each of the possible CPU architecture supported by Docker, unless indicated otherwise.
- Each binary has permissions `500` (read and execute for the user owner)
- You can change the ownership in the `COPY` command using `--chown=1000` for example, without duplicating the binary in your Docker image layers.
- Each Docker image has an entrypoint `[ "/bin" ]` so you can run it as well

**Need help?** ▶️ [Create a discussion](https://github.com/kbuley/binpot/discussions)

[Thinking of copying the binary for your host?](#Copy-the-binary-on-your-host)

## Programs available

|Program|Lastversion|Imagetags|Architectures|
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|-------------------------------|
|[`bit`](https://github.com/chriswalz/bit)|[`v1.1.2`](https://github.com/chriswalz/bit/releases/tag/v1.1.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=bit)|all|
|[`buildx`](https://github.com/docker/buildx)|[`v0.12.0`](https://github.com/docker/buildx/releases/tag/v0.12)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=buildx)|all|
|[`compose`](https://github.com/docker/compose)|[`v2.23.3`](https://github.com/docker/compose/releases/tag/v2.23.3)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=compose)|all|
|[`dlv`](https://github.com/go-delve/delve)|[`v1.21.2`](https://github.com/go-delve/delve/releases/tag/v1.21.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=dlv)|all|
|[`docker`](https://github.com/docker/cli)|[`v24.0.7`](https://github.com/docker/cli/releases/tag/v24.0.7)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=docker)|all|
|[`gh`](https://github.com/cli/cli)|[`v2.40.1`](https://github.com/cli/cli/releases/tag/v2.40.1)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gh)|all|
|[`golangci-lint`](https://github.com/golangci/golangci-lint)|[`v1.55.2`](https://github.com/golangci/golangci-lint/releases/tag/v1.55.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=golangci-lint)|all|
|[`gomock`](https://github.com/golang/mock)|[`v1.6.0`](https://github.com/golang/mock/releases/tag/v1.6.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gomock)|all|
|[`gomodifytags`](https://github.com/fatih/gomodifytags)|[`v1.16.0`](https://github.com/fatih/gomodifytags/releases/tag/v1.16.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gomodifytags)|all|
|[`go-outline`](https://github.com/ramya-rao-a/go-outline)|[`9736a4b`](https://github.com/ramya-rao-a/go-outline/commit/9736a4bde949f321d201e5eaa5ae2bcde011bf00)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=go-outline)|all|
|[`gopkgs`](https://github.com/uudashr/gopkgs)|[`v2.1.2`](https://github.com/uudashr/gopkgs/releases/tag/v2.1.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gopkgs)|all|
|[`goplay`](https://github.com/haya14busa/goplay)|[`v1.0.0`](https://github.com/haya14busa/goplay/releases/tag/v1.0.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=goplay)|all|
|[`gopls`](https://github.com/golang/tools/tree/master/gopls)|[`v0.14.2`](https://github.com/golang/tools/releases/tag/gopls/v0.14.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gopls)|all|
|[`gotests`](https://github.com/cweill/gotests)|[`v1.6.0`](https://github.com/cweill/gotests/releases/tag/v1.6.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=gotests)|all|
|[`helm`](https://github.com/helm/helm)|[`v3.13.3`](https://github.com/helm/helm/releases/tag/v3.13.3)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=helm)|all|
|[`impl`](https://github.com/josharian/impl)|[`v1.2.0`](https://github.com/josharian/impl/releases/tag/v1.2.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=impl)|all|
|[`kubectl`](https://github.com/kubernetes/kubernetes)|[`v1.29.0`](https://github.com/kubernetes/kubernetes/releases/tag/v1.29.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=kubectl)|all|
|[`kubectx`](https://github.com/ahmetb/kubectx)|[`v0.9.5`](https://github.com/ahmetb/kubectx/releases/tag/v0.9.5)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=kubectx)|all|
|[`kubens`](https://github.com/ahmetb/kubectx)|[`v0.9.5`](https://github.com/ahmetb/kubectx/releases/tag/v0.9.5)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=kubens)|all|
|[`logo-ls`](https://github.com/Yash-Handa/logo-ls)|[`v1.3.7`](https://github.com/Yash-Handa/logo-ls/releases/tag/v1.3.7)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=logo-ls-v1.3.7)|all|
|[`mockery`](https://github.com/vektra/mockery)|[`v2.38.0`](https://github.com/vektra/mockery/releases/tag/v2.38.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=mockery)|all|
|[`mockgen`](https://github.com/golang/mock)|[`v1.6.0`](https://github.com/golang/mock/releases/tag/v1.6.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=mockgen)|all|
|[`stern`](https://github.com/stern/stern)|[`v1.27.0`](https://github.com/stern/stern/releases/tag/v1.27.0)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=stern)|all|
|[`supervisord`](https://github.com/ochinchina/supervisord)|[`v0.7.3`](https://github.com/ochinchina/supervisord/releases/tag/v0.7.3)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=supervisord)|all|
|[`lazygit`](https://github.com/jesseduffield/lazygit)|[`v0.40.2`](https://github.com/jesseduffield/lazygit/releases/tag/v0.40.2)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=lazygit)|all|
|[`chezmoi`](https://github.com/twpayne/chezmo)|[`v2.42.3`](https://github.com/twpayne/chezmoi/releases/tag/v2.42.3)|[**DockerHub**](https://hub.docker.com/r/kbuley/binpot/tags?name=lazygit)|all|
ℹ️`all`architecturesmeans:linux/amd64,linux/arm64

**Want more!?** ▶️ [Create an issue!](https://github.com/kbuley/binpot/issues)

## How it works

1. For each program, a Dockerfile describes how to build it. The final binary is placed on a final [scratch](https://hub.docker.com/_/scratch) based Docker image. _Example:_ `helm` has [`./dockerfiles/helm/Dockerfile`](dockerfiles/helm/Dockerfile)
2. For each program, a Github Action workflow is triggered when its Dockerfile or the workflow itself is changed. This workflow takes care of:
   1. Cross build the program for all CPU architectures
   2. Pushing the images containing the program to Docker Hub

## Copy the binary on your host

If you want to use the binary directly on your host, you can do it with Docker.
This has the advantage that it will automatically get the right binary for your host platform.

In the following we want to install `helm` on our host.

For example:

```sh
export PROGRAM="helm" && \
  docker pull "kbuley/binpot:$PROGRAM" && \
  containerid="$(docker create kbuley/binpot:$PROGRAM)" && \
  docker cp "$containerid:/bin" "/usr/local/bin/$PROGRAM" && \
  docker rm "$containerid"
```

Test Helm works with `helm`

## TODOs

- Change version of go-outline once a release tag is made: [Github issue](https://github.com/ramya-rao-a/go-outline/issues/15)
