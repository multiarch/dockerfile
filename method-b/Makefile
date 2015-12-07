TARGET ?= amd64


build: Dockerfile
	docker build --no-cache -t multiarch-dockerfile:$(TARGET)-methodb .
	docker run --rm multiarch-dockerfile:$(TARGET)-methodb uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methodb ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methodb ls -la /overlay


.PHONY: Dockerfile
Dockerfile: Dockerfile.$(TARGET)
	cp $< $@
