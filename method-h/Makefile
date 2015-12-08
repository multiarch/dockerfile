TARGET ?= amd64
FROM_IMAGE ?= multiarch/ubuntu-debootstrap:${TARGET}-wily
# here we can use a dynamic FROM_IMAGE without regularity in the name

build:
	docker build --build-arg "ARCH=$(TARGET)" --build-arg "FROM_IMAGE=$(FROM_IMAGE)" --no-cache -t multiarch-dockerfile:$(TARGET)-methodh .
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methodh ls -la /overlay
