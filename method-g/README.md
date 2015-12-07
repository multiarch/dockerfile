```console
root@fwrz:~/dockerfile/method-g# make TARGET=amd64
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
docker build --build-arg ARCH=amd64 --no-cache -t multiarch-dockerfile:amd64-methode tmp-amd64
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : ARG ARCH=amd64
 ---> Running in f50c4a93dc42
 ---> fb9c65286c53
Removing intermediate container f50c4a93dc42
Step 3 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 3e91a90e640f
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.9 kB]
Fetched 2372 kB in 2s (812 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 0d92c6bf8aa0
Removing intermediate container 3e91a90e640f
Step 4 : RUN echo "I'm ${ARCH}"
 ---> Running in 4bab55d1e83f
I'm amd64
 ---> b4e3a55eb8c7
Removing intermediate container 4bab55d1e83f
Step 5 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in d307f4740adb
This is specific to amd64
 ---> d24db31c506c
Removing intermediate container d307f4740adb
Step 6 : ADD overlay-common /overlay
 ---> 92359bd842d5
Removing intermediate container ebcd1b1ecdcd
Step 7 : ADD overlay-${ARCH} /overlay
 ---> 8c7f9caf6ec9
Removing intermediate container 687eeffcf2f6
Step 8 : CMD uname -a; cowsay hello world
 ---> Running in 9ae1e81b3c57
 ---> a4c0d160719e
Removing intermediate container 9ae1e81b3c57
Successfully built a4c0d160719e
docker run --rm multiarch-dockerfile:amd64-methode uname -a
Linux c79e9338794b 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:32 .
drwxr-xr-x 36 root root 4096 Dec  7 19:32 ..
-rw-r--r--  1 root root    6 Dec  7 19:32 amd64
-rw-r--r--  1 root root    7 Dec  7 19:32 common
```

```console
root@fwrz:~/dockerfile/method-g# make TARGET=powerpc
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
rm -rf tmp-powerpc
mkdir tmp-powerpc
cp Dockerfile tmp-powerpc/Dockerfile
cp -rf overlay-common tmp-powerpc/
cp -rf overlay-powerpc tmp-powerpc/
for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "powerpc" ]; then       \
            sed -i "/arch=$arch/d" tmp-powerpc/Dockerfile;              \
          fi;                                        \
        done
sed -i '/#[[:space:]]*arch=powerpc/s/^#//' tmp-powerpc/Dockerfile
sed -i 's/#[[:space:]]*arch=powerpc//g' tmp-powerpc/Dockerfile
cat tmp-powerpc/Dockerfile
FROM multiarch/ubuntu-debootstrap:powerpc-wily
ARG ARCH=powerpc

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
docker build --build-arg ARCH=powerpc --no-cache -t multiarch-dockerfile:powerpc-methode tmp-powerpc
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : ARG ARCH=powerpc
 ---> Running in a50b1f328d08
 ---> 09096c28d9d8
Removing intermediate container a50b1f328d08
Step 3 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in ac7d9722d3a5
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> fe5d7f3b4835
Removing intermediate container ac7d9722d3a5
Step 4 : RUN echo "I'm ${ARCH}"
 ---> Running in cb1079f53aa0
I'm powerpc
 ---> 37cc85c74b05
Removing intermediate container cb1079f53aa0
Step 5 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 4425eb0e54ef
This is specific to powerpc
 ---> 668288c2c684
Removing intermediate container 4425eb0e54ef
Step 6 : ADD overlay-common /overlay
 ---> 1c855dd28608
Removing intermediate container e96c498ccd49
Step 7 : ADD overlay-${ARCH} /overlay
 ---> 0ff639923c2c
Removing intermediate container e917e9ce1b7c
Step 8 : CMD uname -a; cowsay hello world
 ---> Running in efee286c8730
 ---> 74da414e9bd6
Removing intermediate container efee286c8730
Successfully built 74da414e9bd6
docker run --rm multiarch-dockerfile:powerpc-methode uname -a
Linux 0759ca0a8185 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:33 .
drwxr-xr-x 34 root root 4096 Dec  7 19:33 ..
-rw-r--r--  1 root root    7 Dec  7 19:33 common
-rw-r--r--  1 root root    8 Dec  7 19:33 powerpc
```

```console
root@fwrz:~/dockerfile/method-g# make TARGET=armhf
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
rm -rf tmp-armhf
mkdir tmp-armhf
cp Dockerfile tmp-armhf/Dockerfile
cp -rf overlay-common tmp-armhf/
cp -rf overlay-armhf tmp-armhf/
for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "armhf" ]; then       \
            sed -i "/arch=$arch/d" tmp-armhf/Dockerfile;              \
          fi;                                        \
        done
sed -i '/#[[:space:]]*arch=armhf/s/^#//' tmp-armhf/Dockerfile
sed -i 's/#[[:space:]]*arch=armhf//g' tmp-armhf/Dockerfile
cat tmp-armhf/Dockerfile
FROM multiarch/ubuntu-debootstrap:armhf-wily
ARG ARCH=armhf

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
docker build --build-arg ARCH=armhf --no-cache -t multiarch-dockerfile:armhf-methode tmp-armhf
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : ARG ARCH=armhf
 ---> Running in 54e2f5ce50ff
 ---> d5505a7b9be6
Removing intermediate container 54e2f5ce50ff
Step 3 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 29e1dd008fc7
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 7d8b7c42c44e
Removing intermediate container 29e1dd008fc7
Step 4 : RUN echo "I'm ${ARCH}"
 ---> Running in 075451b32654
I'm armhf
 ---> e86a85032df8
Removing intermediate container 075451b32654
Step 5 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in c0639609fc3f
This is specific to armhf
 ---> 70c00b8b36a1
Removing intermediate container c0639609fc3f
Step 6 : ADD overlay-common /overlay
 ---> e7ba7e48f6ff
Removing intermediate container 44bc8802b3b4
Step 7 : ADD overlay-${ARCH} /overlay
 ---> b38992ca7cf9
Removing intermediate container c9093b4fb9ff
Step 8 : CMD uname -a; cowsay hello world
 ---> Running in 2cd34598e5b7
 ---> 970deffbd03d
Removing intermediate container 2cd34598e5b7
Successfully built 970deffbd03d
docker run --rm multiarch-dockerfile:armhf-methode uname -a
Linux 2273ff95c3bd 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:34 .
drwxr-xr-x 34 root root 4096 Dec  7 19:34 ..
-rw-r--r--  1 root root    6 Dec  7 19:33 armhf
-rw-r--r--  1 root root    7 Dec  7 19:33 common
```