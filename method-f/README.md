```console
root@fwrz:~/dockerfile/method-f# make TARGET=amd64
docker build --build-arg ARCH=amd64 --no-cache -t multiarch-dockerfile:amd64-methodf .
Sending build context to Docker daemon 16.38 kB
Step 1 : FROM scratch
 --->
Step 2 : ARG ARCH=amd64
 ---> Running in de2cf54d1d83
 ---> ff7fabb6bfaa
Removing intermediate container de2cf54d1d83
Step 3 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 4 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 02251f961e4c
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 76ed85eb0b7e
Removing intermediate container 02251f961e4c
Step 5 : RUN echo "I'm ${ARCH}"
 ---> Running in 68b88ba364f3
I'm amd64
 ---> f804a455a4d3
Removing intermediate container 68b88ba364f3
Step 6 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 0bab0c22d991
This is specific to amd64
 ---> 6f80ad5c11c2
Removing intermediate container 0bab0c22d991
Step 7 : ADD overlay-common /overlay
 ---> ddbeb546063c
Removing intermediate container 4a02f31f7115
Step 8 : ADD overlay-${ARCH} /overlay
 ---> 2b0919106171
Removing intermediate container dd03a2578d38
Step 9 : CMD uname -a; cowsay hello world
 ---> Running in ca4696e5f0c1
 ---> de098e3ce683
Removing intermediate container ca4696e5f0c1
Successfully built de098e3ce683
docker run --rm multiarch-dockerfile:amd64-methodf uname -a
Linux 594c0d47c886 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methodf ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methodf ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:21 .
drwxr-xr-x 34 root root 4096 Dec  7 19:21 ..
-rw-r--r--  1 root root    6 Dec  7 18:59 amd64
-rw-r--r--  1 root root    7 Dec  7 18:59 common
```

```console
root@fwrz:~/dockerfile/method-f# make TARGET=armhf
docker build --build-arg ARCH=armhf --no-cache -t multiarch-dockerfile:armhf-methodf .
Sending build context to Docker daemon 16.38 kB
Step 1 : FROM scratch
 --->
Step 2 : ARG ARCH=amd64
 ---> Running in 2ac0a1df618c
 ---> 0b295fe446eb
Removing intermediate container 2ac0a1df618c
Step 3 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 4 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 4b4ddd898b4a
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 9f184658e621
Removing intermediate container 4b4ddd898b4a
Step 5 : RUN echo "I'm ${ARCH}"
 ---> Running in ca561b4da7c9
I'm armhf
 ---> 231a23be9306
Removing intermediate container ca561b4da7c9
Step 6 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 1fc5e0b1d4fe
This is specific to armhf
 ---> 607142c667e0
Removing intermediate container 1fc5e0b1d4fe
Step 7 : ADD overlay-common /overlay
 ---> 39fb23cfcd7b
Removing intermediate container d315279e7a37
Step 8 : ADD overlay-${ARCH} /overlay
 ---> 4a3d14ca1615
Removing intermediate container cca2257dc19b
Step 9 : CMD uname -a; cowsay hello world
 ---> Running in 7be6a8e8f848
 ---> 0f6deae0e3ef
Removing intermediate container 7be6a8e8f848
Successfully built 0f6deae0e3ef
docker run --rm multiarch-dockerfile:armhf-methodf uname -a
Linux a3a5d5e217c6 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methodf ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methodf ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:21 .
drwxr-xr-x 34 root root 4096 Dec  7 19:21 ..
-rw-r--r--  1 root root    6 Dec  7 18:59 armhf
-rw-r--r--  1 root root    7 Dec  7 18:59 common
```

```console
root@fwrz:~/dockerfile/method-f# make TARGET=powerpc
docker build --build-arg ARCH=powerpc --no-cache -t multiarch-dockerfile:powerpc-methodf .
Sending build context to Docker daemon 16.38 kB
Step 1 : FROM scratch
 --->
Step 2 : ARG ARCH=amd64
 ---> Running in d086f23132cf
 ---> e39d89a216ee
Removing intermediate container d086f23132cf
Step 3 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 4 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 36408769e6d5
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 84a1847468cd
Removing intermediate container 36408769e6d5
Step 5 : RUN echo "I'm ${ARCH}"
 ---> Running in 3d32b6b13d8b
I'm powerpc
 ---> 5ebd149e599f
Removing intermediate container 3d32b6b13d8b
Step 6 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 82de5a076a6b
This is specific to powerpc
 ---> e4337210e313
Removing intermediate container 82de5a076a6b
Step 7 : ADD overlay-common /overlay
 ---> 0b8ca9d0ab46
Removing intermediate container 6a285afb6744
Step 8 : ADD overlay-${ARCH} /overlay
 ---> c3380b8abd34
Removing intermediate container ad99e5fa1215
Step 9 : CMD uname -a; cowsay hello world
 ---> Running in ca7a5966e6af
 ---> eaebadc010d8
Removing intermediate container ca7a5966e6af
Successfully built eaebadc010d8
docker run --rm multiarch-dockerfile:powerpc-methodf uname -a
Linux e1cfebadb742 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methodf ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methodf ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 19:22 .
drwxr-xr-x 34 root root 4096 Dec  7 19:22 ..
-rw-r--r--  1 root root    7 Dec  7 18:59 common
-rw-r--r--  1 root root    8 Dec  7 18:59 powerpc
```
