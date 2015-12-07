FROM multiarch/ubuntu-debootstrap:amd64-wily       # arch=amd64
#FROM multiarch/ubuntu-debootstrap:armhf-wily      # arch=armhf
#FROM multiarch/ubuntu-debootstrap:powerpc-wily    # arch=powerpc

ARG ARCH

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN [ "${ARCH}" = "amd64" ] || echo "Special build instruction for amd64"


ADD overlay-common  /overlay
ADD overlay-amd64   /overlay                      # arch=amd64
#ADD overlay-armhf   /overlay                      # arch=armhf
#ADD overlay-powerpc /overlay                      # arch=powerpc

CMD ["uname -a; cowsay hello world"]
