Dockerfile-gox 
====

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)][LICENSE]
[![Docker Pulls](https://img.shields.io/docker/pulls/tcnksm/gox.svg?style=flat-square)][dockerhub]

[LICENSE]: https://github.com/tcnksm/dockerfile-gox/blob/master/LICENCE
[dockerhub]: https://registry.hub.docker.com/u/tcnksm/gox/

Dockerfile for Cross-compiling golang project with [mitchellh/gox](https://github.com/mitchellh/gox).

## Description

[docker-library/golang](https://github.com/docker-library/golang) (Docker official golang stack) also support image for cross-compile. With `Dockerfile-gox`, You can cross-compile your golang project parallelly. It's more fast when compiling for multiple platform.

## Supported tags

`tcnksm/gox` image support below tags. Link is its `Dockerfile`. 

- [`1.2.2` (1.2.2/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.2.2/Dockerfile)
- [`1.3` (1.3/Docekerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.3/Dockerfile)
- [`1.3.1` (1.3.1/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.3.1/Dockerfile)
- [`1.3.2` (1.3.2/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.3.2/Dockerfile)
- [`1.4` (1.4/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.4/Dockerfile)
- [`1.4.1` (1.4.1/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.4/Dockerfile)
- [`1.4.2` (1.4.2/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.4.2/Dockerfile)
- [`1.5-beta` (1.5-beta/Dockerfile)](https://github.com/tcnksm/dockerfile-gox/blob/master/1.5-beta/Dockerfile) (Experimental)


Tag is correspond to its golang version. 

### Go1.5 is awesome

[Cross compilation just got a whole lot better in Go 1.5](http://dave.cheney.net/2015/03/03/cross-compilation-just-got-a-whole-lot-better-in-go-1-5)

From Go1.5, you don't need to build target platform build toolchain before using gox. So image size is really small. Below is size difference between `1.4.2` and `1.5-beta`, 

```bash
$ docker images
tcnksm/gox                                         1.4.2               6b0db9c28a1a        4 months ago        1.787 GB
tcnksm/gox                                         1.5-beta            478032add391        5 hours ago         595.6 MB
```

**NOTE** `1.5-beta` will be replaced with 1.5 after released.

## Usage

If you want to cross-compile with go v1.3.1:

```bash
$ docker run --rm -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp tcnksm/gox:1.3.1 
```

Or if you want to cross-compile with go v1.2:

```bash
$ docker run --rm -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp tcnksm/gox:1.2 
```

You can overwrite command. If you have Makefile with `gox`:

```bash
$ docker run --rm -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp tcnksm/gox:1.3.1 make 
```

Or if you want to build for 64-bit linux and change output to `pkg` directory with your favor name:

```bash
$ docker run --rm -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp tcnksm/gox:1.3.1 gox -osarch="linux/amd64" -output "pkg/{{.OS}}_{{.Arch}}/{{.Dir}}"
```

If you want to know `gox` arguments more, See documents in [mitchellh/gox](https://github.com/mitchellh/gox).

## light image

`light` tag provide light image. It only provides `linux` and `darwin`, `windows` build-chain. If you don't need other platform, use this image. You can use it in same way as ordinal one. 

Here is image size comparison, 

```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
tcnksm/gox          1.4.2               98d4147293ca        23 seconds ago      1.787 GB
tcnksm/gox          1.4.2-light         9e30b7109b86        5 minutes ago       533.1 MB
```

## Contribution

1. Fork ([https://github.com/tcnksm/dockerfile-gox/fork](https://github.com/tcnksm/dockerfile-gox/fork))
1. Create a feature branch
1. Commit your changes
1. Rebase your local changes against the master branch
1. Push it to your remote repository
1. Create new Pull Request

## Author

[tcnksm](https://github.com/tcnksm)
