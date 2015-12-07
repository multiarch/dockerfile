```console
root@fwrz:~/dockerfile/method-a# make TARGET=powerpc
$ cp Dockerfile.multiarch Dockerfile
$ for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "powerpc" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
$ sed -i 's/#[[:space:]]*arch=powerpc//g' Dockerfile
$ cat Dockerfile
FROM multiarch/ubuntu-debootstrap:powerpc-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm powerpc"

ADD overlay-common  /overlay
ADD overlay-powerpc /overlay

CMD ["uname -a; cowsay hello world"]
$ docker build --no-cache -t multiarch-dockerfile:powerpc-methoda .
Sending build context to Docker daemon 22.53 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in f78871314022
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 59404413b764
Removing intermediate container f78871314022
Step 3 : RUN echo "I'm powerpc"
 ---> Running in a26ba1ff3d6e
I'm powerpc
 ---> 86b8b14153b0
Removing intermediate container a26ba1ff3d6e
Step 4 : ADD overlay-common /overlay
 ---> 49a81d9dbdfc
Removing intermediate container 49c8b95641cf
Step 5 : ADD overlay-powerpc /overlay
 ---> 7d9cf3c46424
Removing intermediate container 1e6689f2ed0c
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 8ab55a15a06e
 ---> 2e422ef7c180
Removing intermediate container 8ab55a15a06e
Successfully built 2e422ef7c180
$ docker run --rm multiarch-dockerfile:powerpc-methoda uname -a
Linux cf6c72b30773 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
$ docker run --rm multiarch-dockerfile:powerpc-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
$ docker run --rm multiarch-dockerfile:powerpc-methoda ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:26 .
drwxr-xr-x 34 root root 4096 Dec  7 17:26 ..
-rw-r--r--  1 root root    7 Dec  7 17:26 common
-rw-r--r--  1 root root    8 Dec  7 17:26 powerpc
```

```console
root@fwrz:~/dockerfile/method-a# make TARGET=armhf
$ cp Dockerfile.multiarch Dockerfile
$ for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "armhf" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
$ sed -i 's/#[[:space:]]*arch=armhf//g' Dockerfile
$ cat Dockerfile
FROM multiarch/ubuntu-debootstrap:armhf-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm arhmf"

ADD overlay-common  /overlay
ADD overlay-armhf   /overlay

CMD ["uname -a; cowsay hello world"]
$ docker build --no-cache -t multiarch-dockerfile:armhf-methoda .
Sending build context to Docker daemon 22.53 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in ba2ad932f621
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> b6102124c6b2
Removing intermediate container ba2ad932f621
Step 3 : RUN echo "I'm arhmf"
 ---> Running in e6c8fbd8ddef
I'm arhmf
 ---> a4741a22b7d8
Removing intermediate container e6c8fbd8ddef
Step 4 : ADD overlay-common /overlay
 ---> aef304397140
Removing intermediate container 9c89de07b8f4
Step 5 : ADD overlay-armhf /overlay
 ---> 64e2e3512d32
Removing intermediate container 70891364d5d2
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in cdfd324a0ec4
 ---> 3b05c7c87bf1
Removing intermediate container cdfd324a0ec4
Successfully built 3b05c7c87bf1
$ docker run --rm multiarch-dockerfile:armhf-methoda uname -a
Linux 859075ed5622 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
$ docker run --rm multiarch-dockerfile:armhf-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
$ docker run --rm multiarch-dockerfile:armhf-methoda ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:27 .
drwxr-xr-x 34 root root 4096 Dec  7 17:27 ..
-rw-r--r--  1 root root    6 Dec  7 17:26 armhf
-rw-r--r--  1 root root    7 Dec  7 17:26 common
```

```console
root@fwrz:~/dockerfile/method-a# make TARGET=amd64
$ cp Dockerfile.multiarch Dockerfile
$ for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "amd64" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
$ sed -i 's/#[[:space:]]*arch=amd64//g' Dockerfile
$ cat Dockerfile
FROM multiarch/ubuntu-debootstrap:amd64-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm amd64"

ADD overlay-common  /overlay
ADD overlay-amd64   /overlay

CMD ["uname -a; cowsay hello world"]
$ docker build --no-cache -t multiarch-dockerfile:amd64-methoda .
Sending build context to Docker daemon 22.53 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in ab74e23531fc
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.3 kB]
Fetched 2370 kB in 1s (1472 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 7f80761c3adb
Removing intermediate container ab74e23531fc
Step 3 : RUN echo "I'm amd64"
 ---> Running in e48d619fb49a
I'm amd64
 ---> b8d29f9a3488
Removing intermediate container e48d619fb49a
Step 4 : ADD overlay-common /overlay
 ---> af283c9ef176
Removing intermediate container c61ade2723fd
Step 5 : ADD overlay-amd64 /overlay
 ---> 5dc0912a2ff8
Removing intermediate container 55a112533eaa
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 62f07922c8bb
 ---> 1ac9e323a08b
Removing intermediate container 62f07922c8bb
Successfully built 1ac9e323a08b
$ docker run --rm multiarch-dockerfile:amd64-methoda uname -a
Linux 5a7b53e84071 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
$ docker run --rm multiarch-dockerfile:amd64-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
$ docker run --rm multiarch-dockerfile:amd64-methoda ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:27 .
drwxr-xr-x 36 root root 4096 Dec  7 17:27 ..
-rw-r--r--  1 root root    6 Dec  7 17:26 amd64
-rw-r--r--  1 root root    7 Dec  7 17:26 common
```
