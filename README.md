#Binpot

Thestaticallycompiled,crossarchitecture,Dockerbased,binariespot.

<imgheight="150"src="https://raw.githubusercontent.com/kbuley/binpot/main/binpot.svg">

[Blogpost](https://qqq.ninja/blog/post/binpot/)

[![MIT](https://img.shields.io/github/license/kbuley/binpot)](https://github.com/kbuley/binpot/main/LICENSE)

##Usage

TheusageisfocusedtobuildotherDockerimages.

Forexample:

```Dockerfile
FROMalpine:3.14
COPY--from=kbuley/binpot:helm/bin/usr/local/bin/helm
```

[🔍Searchforallimagetags💡](https://hub.docker.com/r/kbuley/binpot/tags)

-TheDockerimagetagsfor`kbuley/binpot`followthefollowingformatting:
-`:name`forthelateststableversionoftheprogram`name`
-`:name-v0.0.0`forthesemverversionoftheprogram`name`
-EachDockerimageisbasedon[scratch](https://hub.docker.com/_/scratch)andonlycontainthebinaryprogramatthepath`/bin`.
-EachDockerimageandbinaryprogramisbuiltforeachofthepossibleCPUarchitecturesupportedbyDocker,unlessindicatedotherwise.
-Eachbinaryhaspermissions`500`(readandexecutefortheuserowner)
-Youcanchangetheownershipinthe`COPY`commandusing`--chown=1000`forexample,withoutduplicatingthebinaryinyourDockerimagelayers.
-EachDockerimagehasanentrypoint`["/bin"]`soyoucanrunitaswell

**Needhelp?**▶️[Createadiscussion](https://github.com/kbuley/binpot/discussions)

[Thinkingofcopyingthebinaryforyourhost?](#Copy-the-binary-on-your-host)

##Programsavailable

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

**Wantmore!?**▶️[Createanissue!](https://github.com/kbuley/binpot/issues)

##Howitworks

1.Foreachprogram,aDockerfiledescribeshowtobuildit.Thefinalbinaryisplacedonafinal[scratch](https://hub.docker.com/_/scratch)basedDockerimage._Example:_`helm`has[`./dockerfiles/helm/Dockerfile`](dockerfiles/helm/Dockerfile)
2.Foreachprogram,aGithubActionworkflowistriggeredwhenitsDockerfileortheworkflowitselfischanged.Thisworkflowtakescareof:
1.CrossbuildtheprogramforallCPUarchitectures
2.PushingtheimagescontainingtheprogramtoDockerHub

##Copythebinaryonyourhost

Ifyouwanttousethebinarydirectlyonyourhost,youcandoitwithDocker.
Thishastheadvantagethatitwillautomaticallygettherightbinaryforyourhostplatform.

Inthefollowingwewanttoinstall`helm`onourhost.

Forexample:

```sh
exportPROGRAM="helm"&&\
dockerpull"kbuley/binpot:$PROGRAM"&&\
containerid="$(dockercreatekbuley/binpot:$PROGRAM)"&&\
dockercp"$containerid:/bin""/usr/local/bin/$PROGRAM"&&\
dockerrm"$containerid"
```

TestHelmworkswith`helm`

##TODOs

-Changeversionofgo-outlineonceareleasetagismade:[Githubissue](https://github.com/ramya-rao-a/go-outline/issues/15)
