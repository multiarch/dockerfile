```console
root@fwrz:~/dockerfile/method-a# make TARGET=amd64
cp Dockerfile.multiarch Dockerfile
for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "amd64" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
sed -i 's/#[[:space:]]*arch=amd64//g' Dockerfile
cat Dockerfile
FROM multiarch/ubuntu-debootstrap:amd64-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm amd64"

CMD ["uname -a; cowsay hello world"]
docker build --no-cache -t multiarch-dockerfile:amd64-methoda .
Sending build context to Docker daemon 6.656 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in b3978be51325
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.3 kB]
Fetched 2370 kB in 13s (180 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 15b68e6a5071
Removing intermediate container b3978be51325
Step 3 : RUN echo "I'm amd64"
 ---> Running in a9afcd7d739b
I'm amd64
 ---> 35989a5efb6b
Removing intermediate container a9afcd7d739b
Step 4 : CMD uname -a; cowsay hello world
 ---> Running in 873723f8f1a0
 ---> eeeb6f0dd331
Removing intermediate container 873723f8f1a0
Successfully built eeeb6f0dd331
docker run --rm multiarch-dockerfile:amd64-methoda uname -a
Linux 911ae85210c7 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
```

```console
root@fwrz:~/dockerfile/method-a# make TARGET=armhf
cp Dockerfile.multiarch Dockerfile
for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "armhf" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
sed -i 's/#[[:space:]]*arch=armhf//g' Dockerfile
cat Dockerfile
FROM multiarch/ubuntu-debootstrap:armhf-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm arhmf"

CMD ["uname -a; cowsay hello world"]
docker build --no-cache -t multiarch-dockerfile:armhf-methoda .
Sending build context to Docker daemon 6.656 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 53b40209092f
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 050d0523a74e
Removing intermediate container 53b40209092f
Step 3 : RUN echo "I'm arhmf"
 ---> Running in 5eb1b6ef0d28
I'm arhmf
 ---> 5d738d01338b
Removing intermediate container 5eb1b6ef0d28
Step 4 : CMD uname -a; cowsay hello world
 ---> Running in bce7c33bbf75
 ---> db845e4af8b2
Removing intermediate container bce7c33bbf75
Successfully built db845e4af8b2
docker run --rm multiarch-dockerfile:armhf-methoda uname -a
Linux 23e2322fe295 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
```

```console
root@fwrz:~/dockerfile/method-a# make TARGET=powerpc
cp Dockerfile.multiarch Dockerfile
for arch in amd64 armhf powerpc; do                     \
          if [ "$arch" != "powerpc" ]; then       \
            sed -i "/arch=$arch/d" Dockerfile;              \
          fi;                                        \
        done
sed -i 's/#[[:space:]]*arch=powerpc//g' Dockerfile
cat Dockerfile
FROM multiarch/ubuntu-debootstrap:powerpc-wily

RUN apt-get update && apt-get install --no-install-recommends -y -q wget

RUN echo "I'm powerpc"

CMD ["uname -a; cowsay hello world"]
docker build --no-cache -t multiarch-dockerfile:powerpc-methoda .
Sending build context to Docker daemon 6.656 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 75f3619b2904
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 9b7229817f43
Removing intermediate container 75f3619b2904
Step 3 : RUN echo "I'm powerpc"
 ---> Running in 6b06d5941820
I'm powerpc
 ---> 368ecba81ac4
Removing intermediate container 6b06d5941820
Step 4 : CMD uname -a; cowsay hello world
 ---> Running in 7de1b74b25f3
 ---> 8a9c68c82f62
Removing intermediate container 7de1b74b25f3
Successfully built 8a9c68c82f62
docker run --rm multiarch-dockerfile:powerpc-methoda uname -a
Linux 11e656b836bc 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methoda ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
```
