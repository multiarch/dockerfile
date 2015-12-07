FROM scratch
ARG ARCH=amd64

# FROM multiarch/ubuntu-debootstrap:$ARCH-wily
# sadly, it does not work :(
FROM multiarch/ubuntu-debootstrap:armhf-wily

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
