ARG "REGISTRY=multiarch/ubuntu-debootstrap ARCH=amd64"
#
# We need to patch docker to handle ARG before FROM
#
FROM ${REGISTRY}:${ARCH}-wily

RUN apt-get update \
 && apt-get install --no-install-recommends -y -q wget

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
        echo "${ARCH} not supported yet"     \
      ;;                                     \
      esac


ADD overlay-common    /overlay
ADD overlay-${ARCH}   /overlay

CMD ["uname -a; cowsay hello world"]
