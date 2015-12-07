TARGET ?= amd64
BASE_ARCH = amd64


build: tmp-$(TARGET)/Dockerfile
	docker build --no-cache -t multiarch-dockerfile:$(TARGET)-methodc tmp-$(TARGET)
	docker run --rm multiarch-dockerfile:$(TARGET)-methodc uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methodc ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methodc ls -la /overlay


tmp-$(TARGET)/Dockerfile: Dockerfile $(shell find overlay-common overlay-$(TARGET))
	rm -rf tmp-$(TARGET)
	mkdir tmp-$(TARGET)
	cp Dockerfile $@
	cp -rf overlay-common tmp-$(TARGET)/
	cp -rf overlay-$(TARGET) tmp-$(TARGET)/
	if [ "$(TARGET)" != "$(BASE_ARCH)" ]; then   \
	  sed -i "s/$(BASE_ARCH)/$(TARGET)/g" $@;    \
	fi
