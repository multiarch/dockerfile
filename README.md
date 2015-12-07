# dockerfile
Multiarch Dockerfile POC

## method A

## method B

## method C

* `Dockerfile` is written for `amd64`
* running `make` will:
  * create a `tmp-$(ARCH)` directory
  * copy `overlay-common` + `overlay-$(ARCH)`
  * copy `Dockerfile` if `TARGET` is `amd64`, else it will replace all occurences of `amd64` with `$(TARGET)`

Pros
* The Dockerfile works out of the box without our Makefile system

Cons
* May be difficult (or impossible) to write "multiarch" Dockerfile (sometimes, we need to replace with `armhf`, sometimes with `armv7l`, sometimes with `arm`, ...)
