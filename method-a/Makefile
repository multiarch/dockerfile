TARGET ?= amd64
ARCHS ?= amd64 armhf powerpc


build: Dockerfile
	docker build --no-cache -t multiarch-dockerfile:$(TARGET)-methoda .
	docker run --rm multiarch-dockerfile:$(TARGET)-methoda uname -a
	docker run --rm multiarch-dockerfile:$(TARGET)-methoda ls -la /usr/bin/wget


.PHONY: Dockerfile
Dockerfile: Dockerfile.multiarch
	cp $< $@
	for arch in $(ARCHS); do                     \
	  if [ "$$arch" != "$(TARGET)" ]; then       \
	    sed -i "/arch=$$arch/d" $@;              \
	  fi;                                        \
	done
	sed -i 's/#[[:space:]]*arch=$(TARGET)//g' $@
	cat $@
