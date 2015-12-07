FROM multiarch/ubuntu-debootstrap:amd64-wily       # arch=amd64
#FROM multiarch/ubuntu-debootstrap:armhf-wily      # arch=armhf
#FROM multiarch/ubuntu-debootstrap:powerpc-wily    # arch=powerpc
ARG ARCH=amd64					   # arch=amd64
#ARG ARCH=armhf					   # arch=armhf
#ARG ARCH=powerpc				   # arch=powerpc

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm ${ARCH}"

RUN case "${ARCH}" in                        \
      armhf)                                 \
        echo "This is specific to armhf"     \
      ;;                                     \
      amd64)                                 \
        echo "This is specific to amd64"     \
      ;;                                     \
      powerpc)                               \
        echo "This is specific to powerpc"   \
      ;;                                     \
      *)                                     \
        echo "This is the default"           \
      ;;                                     \
      esac
    
ADD overlay-common      /overlay
ADD overlay-${ARCH}   /overlay

CMD ["uname -a; cowsay hello world"]
