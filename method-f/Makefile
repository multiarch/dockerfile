TARGET ?= amd64
ARCHS ?= amd64 armhf powerpc
BASE_ARCH ?= amd64


build:
	docker build --build-arg ARCH=$(TARGET) --no-cache -t multiarch-dockerfile:$(TARGET)-methodf .
	docker run --rm multiarch-dockerfile:$(TARGET)-methodf uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methodf ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methodf ls -la /overlay
