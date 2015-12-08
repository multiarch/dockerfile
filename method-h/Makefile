TARGET ?= amd64
REGISTRY ?= multiarch/ubuntu-debootstrap

build:
	docker build --build-arg "ARCH=$(TARGET) REGISTRY=$(REGISTRY)" --no-cache -t multiarch-dockerfile:$(TARGET)-methodh .
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh ls -la /overlay
