```console
root@fwrz:~/dockerfile/method-g# make TARGET=armhf
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
docker build --build-arg ARCH=armhf --no-cache -t multiarch-dockerfile:armhf-methode tmp-armhf
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 3 : ARG ARCH=amd64
 ---> Running in 451f3fbc3238
 ---> 954f65bd0ecf
Removing intermediate container 451f3fbc3238
Step 4 : RUN apt-get update  && apt-get install --no-install-recommends -y -q wget
 ---> Running in 5f9bf2cedad4
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 6f61bc67fa65
Removing intermediate container 5f9bf2cedad4
Step 5 : RUN echo "I'm ${ARCH}"
 ---> Running in 9547130ff96a
I'm armhf
 ---> 760560e6f234
Removing intermediate container 9547130ff96a
Step 6 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 577715f75884
This is specific to armhf
 ---> 038d2990576d
Removing intermediate container 577715f75884
Step 7 : ADD overlay-common /overlay
 ---> 1dbae8e82685
Removing intermediate container d6bf49a0b4e3
Step 8 : ADD overlay-${ARCH} /overlay
 ---> 3e342d07f328
Removing intermediate container 5c920f6e3225
Step 9 : CMD uname -a; cowsay hello world
 ---> Running in 4cf61dc695e4
 ---> 612ce135a010
Removing intermediate container 4cf61dc695e4
Successfully built 612ce135a010
docker run --rm multiarch-dockerfile:armhf-methode uname -a
Linux f49278430139 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 20:03 .
drwxr-xr-x 34 root root 4096 Dec  7 20:03 ..
-rw-r--r--  1 root root    6 Dec  7 19:53 armhf
-rw-r--r--  1 root root    7 Dec  7 19:53 common
```

```console
root@fwrz:~/dockerfile/method-g# make TARGET=powerpc
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
docker build --build-arg ARCH=powerpc --no-cache -t multiarch-dockerfile:powerpc-methode tmp-powerpc
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 3 : ARG ARCH=amd64
 ---> Running in 275158c418f9
 ---> f214d0c7aafd
Removing intermediate container 275158c418f9
Step 4 : RUN apt-get update  && apt-get install --no-install-recommends -y -q wget
 ---> Running in a3995bce58db
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 18dd9aab21cc
Removing intermediate container a3995bce58db
Step 5 : RUN echo "I'm ${ARCH}"
 ---> Running in 5dda6c6e8194
I'm powerpc
 ---> 115e5f611f4a
Removing intermediate container 5dda6c6e8194
Step 6 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in 9303e6975969
This is specific to powerpc
 ---> 204a2a981fae
Removing intermediate container 9303e6975969
Step 7 : ADD overlay-common /overlay
 ---> 824dc2468e91
Removing intermediate container e83b4329fe3e
Step 8 : ADD overlay-${ARCH} /overlay
 ---> 95a7d0a11137
Removing intermediate container 33860765a839
Step 9 : CMD uname -a; cowsay hello world
 ---> Running in 48ba9fddb923
 ---> 10cd761df745
Removing intermediate container 48ba9fddb923
Successfully built 10cd761df745
docker run --rm multiarch-dockerfile:powerpc-methode uname -a
Linux e0e7d24e5f2f 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 20:04 .
drwxr-xr-x 34 root root 4096 Dec  7 20:04 ..
-rw-r--r--  1 root root    7 Dec  7 20:03 common
-rw-r--r--  1 root root    8 Dec  7 20:03 powerpc
```

```console
root@fwrz:~/dockerfile/method-g# make TARGET=amd64
Makefile:14: warning: overriding commands for target `build'
Makefile:7: warning: ignoring old commands for target `build'
docker build --build-arg ARCH=amd64 --no-cache -t multiarch-dockerfile:amd64-methode tmp-amd64
Sending build context to Docker daemon 5.632 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : ARG ARCH=amd64
 ---> Running in 43400509900c
 ---> 45b55a6bb570
Removing intermediate container 43400509900c
Step 3 : RUN apt-get update  && apt-get install --no-install-recommends -y -q wget
 ---> Running in 3c3a1233ce61
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.9 kB]
Fetched 2372 kB in 2s (801 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 539352645d82
Removing intermediate container 3c3a1233ce61
Step 4 : RUN echo "I'm ${ARCH}"
 ---> Running in 52bcfcdab0d5
I'm amd64
 ---> bb337d0c145f
Removing intermediate container 52bcfcdab0d5
Step 5 : RUN case "${ARCH}" in                              armhf)                                         echo "This is specific to armhf"           ;;                                           amd64)                                         echo "This is specific to amd64"           ;;                                           powerpc)                                       echo "This is specific to powerpc"         ;;                                           *)                                             echo "This is the default"                 ;;                                           esac
 ---> Running in be0d1c695aa2
This is specific to amd64
 ---> d6babd5f5480
Removing intermediate container be0d1c695aa2
Step 6 : ADD overlay-common /overlay
 ---> 3cde78778c7a
Removing intermediate container f51eb2d1a41d
Step 7 : ADD overlay-${ARCH} /overlay
 ---> 9e281c6d9dc8
Removing intermediate container 0315d12bdc6a
Step 8 : CMD uname -a; cowsay hello world
 ---> Running in 24a4742d0e8e
 ---> c0ecdb82eeb2
Removing intermediate container 24a4742d0e8e
Successfully built c0ecdb82eeb2
docker run --rm multiarch-dockerfile:amd64-methode uname -a
Linux b4ebc5255408 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 20:04 .
drwxr-xr-x 36 root root 4096 Dec  7 20:04 ..
-rw-r--r--  1 root root    6 Dec  7 19:53 amd64
-rw-r--r--  1 root root    7 Dec  7 19:53 common
```
