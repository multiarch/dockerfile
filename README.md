# dockerfile
Multiarch Dockerfile POC

## method A

Pros
* Unique Dockerfile
* Gentle about disk usage

Cons
* Don't work out of the box (`docker build` without `Makefile`)
* May be harder to read
* Bad multiline support

---

## method B

Pros
* Dockerfiles are easy to read (one Dockerfile for one architecture, without `sed` at build-time)
* Gentle about disk usage

Cons
* Multiple Dockerfiles, harder to apply a common change

---

## method C

* `Dockerfile` is written for `amd64`
* running `make` will:
  * create a `tmp-$(ARCH)` directory
  * copy `overlay-common` + `overlay-$(ARCH)`
  * copy `Dockerfile` if `TARGET` is `amd64`, else it will replace all occurences of `amd64` with `$(TARGET)`

Pros
* Unique Dockerfile
* The Dockerfile works out of the box without our Makefile system (`docker build`)

Cons
* May be difficult (or impossible) to write "multiarch" Dockerfile (sometimes, we need to replace with `armhf`, sometimes with `armv7l`, sometimes with `arm`, ...)
* Need to copy the whole workspace for each arch on build (take more disk space)
* Bad multiline support


---

## method E

A mix between `method A` and `method C`

Pros
* Unique `Dockerfile`
* The `Dockerfile` is written for `amd64` and works out of the box without the Makefile

Cons
* Need to copy the whole workspace for each arch on build (take more disk space)
* Bad multiline support
