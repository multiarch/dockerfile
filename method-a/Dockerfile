FROM multiarch/ubuntu:amd64-wily      # arch=amd64
FROM multiarch/ubuntu:armhf-wily      # arch=armhf
FROM multiarch/ubuntu:powerpc-wily    # arch=powerpc

RUN apt-get install cowsay

CMD ["uname -a; cowsay hello world"]
