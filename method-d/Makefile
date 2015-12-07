TARGET ?= amd64
ARCHS ?= amd64 armhf powerpc
BASE_ARCH ?= amd64


build: tmp-$(TARGET)/Dockerfile
	docker build --no-cache -t multiarch-dockerfile:$(TARGET)-methode tmp-$(TARGET)
	docker run --rm multiarch-dockerfile:$(TARGET)-methode uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methode ls -la /usr/bin/wget
	docker run --rm multiarch-dockerfile:$(TARGET)-methode ls -la /overlay


tmp-$(TARGET)/Dockerfile: Dockerfile $(shell find overlay-common overlay-$(TARGET))
	rm -rf tmp-$(TARGET)
	mkdir tmp-$(TARGET)
	cp Dockerfile $@
	cp -rf overlay-common tmp-$(TARGET)/
	cp -rf overlay-$(TARGET) tmp-$(TARGET)/
	for arch in $(ARCHS); do                     \
	  if [ "$$arch" != "$(TARGET)" ]; then       \
	    sed -i "/arch=$$arch/d" $@;              \
	  fi;                                        \
	done
	sed -i '/#[[:space:]]*arch=$(TARGET)/s/^#//' $@
	sed -i 's/#[[:space:]]*arch=$(TARGET)//g' $@
	sed -i 's/#[[:space:]]*arch=$(TARGET)//g' $@
	cat $@
