```console
root@fwrz:~/dockerfile/method-c# make TARGET=powerpc
docker build --no-cache -t multiarch-dockerfile:powerpc-methodc tmp-powerpc
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 7e61397a6a8f
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 91e3ef12ee5f
Removing intermediate container 7e61397a6a8f
Step 3 : RUN echo "I'm powerpc"
 ---> Running in 95695d836be3
I'm powerpc
 ---> 03ea5d22dd86
Removing intermediate container 95695d836be3
Step 4 : ADD overlay-common /overlay
 ---> dc370bd770a0
Removing intermediate container ae58abf7930a
Step 5 : ADD overlay-powerpc /overlay
 ---> 76aa634582b2
Removing intermediate container 5d61ff801ae5
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in d0c6115fb030
 ---> 60929b1c1af3
Removing intermediate container d0c6115fb030
Successfully built 60929b1c1af3
docker run --rm multiarch-dockerfile:powerpc-methodc uname -a
Linux d65c3c2fd881 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methodc ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methodc ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:50 .
drwxr-xr-x 34 root root 4096 Dec  7 17:50 ..
-rw-r--r--  1 root root    7 Dec  7 17:50 common
-rw-r--r--  1 root root    8 Dec  7 17:50 powerpc
```

```console
root@fwrz:~/dockerfile/method-c# make TARGET=armhf
rm -rf tmp-armhf
mkdir tmp-armhf
cp Dockerfile tmp-armhf/Dockerfile
cp -rf overlay-common tmp-armhf/
cp -rf overlay-armhf tmp-armhf/
if [ "armhf" != "amd64" ]; then   \
          sed -i "s/amd64/armhf/g" tmp-armhf/Dockerfile;    \
        fi
docker build --no-cache -t multiarch-dockerfile:armhf-methodc tmp-armhf
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 56fa7846b29c
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 85f17ffb2d98
Removing intermediate container 56fa7846b29c
Step 3 : RUN echo "I'm armhf"
 ---> Running in 3c6299162a20
I'm armhf
 ---> 57282dedf806
Removing intermediate container 3c6299162a20
Step 4 : ADD overlay-common /overlay
 ---> d4ba6c3bb7e3
Removing intermediate container 9af89635b120
Step 5 : ADD overlay-armhf /overlay
 ---> a2f6ae06dd2d
Removing intermediate container e1b7ae2f7cf2
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 295fc71da0a9
 ---> 030769d36c96
Removing intermediate container 295fc71da0a9
Successfully built 030769d36c96
docker run --rm multiarch-dockerfile:armhf-methodc uname -a
Linux 90b3d10ba26a 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methodc ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methodc ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:51 .
drwxr-xr-x 34 root root 4096 Dec  7 17:51 ..
-rw-r--r--  1 root root    6 Dec  7 17:50 armhf
-rw-r--r--  1 root root    7 Dec  7 17:50 common
```

```console
root@fwrz:~/dockerfile/method-c# make TARGET=amd64
docker build --no-cache -t multiarch-dockerfile:amd64-methodc tmp-amd64
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 74182719491f
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.3 kB]
Fetched 2370 kB in 2s (802 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 0bec7cdca897
Removing intermediate container 74182719491f
Step 3 : RUN echo "I'm amd64"
 ---> Running in 383faaa4311b
I'm amd64
 ---> c78b30158d0e
Removing intermediate container 383faaa4311b
Step 4 : ADD overlay-common /overlay
 ---> 9cd13c999158
Removing intermediate container 0be40172b307
Step 5 : ADD overlay-amd64 /overlay
 ---> e7a3e637701f
Removing intermediate container 700dbe00cc82
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in a1e8c0065b92
 ---> 44c88be9275d
Removing intermediate container a1e8c0065b92
Successfully built 44c88be9275d
docker run --rm multiarch-dockerfile:amd64-methodc uname -a
Linux 2a22f4e1c91a 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methodc ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methodc ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:51 .
drwxr-xr-x 36 root root 4096 Dec  7 17:51 ..
-rw-r--r--  1 root root    6 Dec  7 17:51 amd64
-rw-r--r--  1 root root    7 Dec  7 17:51 common
```
