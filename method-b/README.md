```console
root@fwrz:~/dockerfile/method-b# make TARGET=amd64
cp Dockerfile.amd64 Dockerfile
docker build --no-cache -t multiarch-dockerfile:amd64-methodb .
Sending build context to Docker daemon 13.31 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 3a584ab356c6
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.3 kB]
Fetched 2370 kB in 3s (780 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> ed9bf4e6420d
Removing intermediate container 3a584ab356c6
Step 3 : RUN echo "I'm amd64"
 ---> Running in 8fee7ba18241
I'm amd64
 ---> de30f64fd673
Removing intermediate container 8fee7ba18241
Step 4 : ADD overlay-common /overlay
 ---> 0148ecbf5660
Removing intermediate container 6f5b5b74a027
Step 5 : ADD overlay-amd64 /overlay
 ---> b6f786d1786a
Removing intermediate container 72eafc0b9bd0
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in b052c1a023eb
 ---> 6744831add51
Removing intermediate container b052c1a023eb
Successfully built 6744831add51
docker run --rm multiarch-dockerfile:amd64-methodb uname -a
Linux 67da5b14844e 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methodb ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methodb ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:33 .
drwxr-xr-x 36 root root 4096 Dec  7 17:33 ..
-rw-r--r--  1 root root    6 Dec  7 17:32 amd64
-rw-r--r--  1 root root    7 Dec  7 17:32 common
```

```console
root@fwrz:~/dockerfile/method-b# make TARGET=armhf
cp Dockerfile.armhf Dockerfile
docker build --no-cache -t multiarch-dockerfile:armhf-methodb .
Sending build context to Docker daemon 13.31 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 4bd9226e5a8a
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 135f6dc0ebb4
Removing intermediate container 4bd9226e5a8a
Step 3 : RUN echo "I'm armhf"
 ---> Running in 7f10c60d3290
I'm armhf
 ---> 77946dc3f2f6
Removing intermediate container 7f10c60d3290
Step 4 : ADD overlay-common /overlay
 ---> 3c5cdb4a812d
Removing intermediate container e9b55bd28fec
Step 5 : ADD overlay-armhf /overlay
 ---> f7b64ee3c79d
Removing intermediate container 5d839a039d42
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 94d40dcfaab3
 ---> 5718d769e499
Removing intermediate container 94d40dcfaab3
Successfully built 5718d769e499
docker run --rm multiarch-dockerfile:armhf-methodb uname -a
Linux 915b82824bbe 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methodb ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methodb ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:40 .
drwxr-xr-x 34 root root 4096 Dec  7 17:40 ..
-rw-r--r--  1 root root    6 Dec  7 17:32 armhf
-rw-r--r--  1 root root    7 Dec  7 17:32 common
```

```console
root@fwrz:~/dockerfile/method-b# make TARGET=powerpc
cp Dockerfile.powerpc Dockerfile
docker build --no-cache -t multiarch-dockerfile:powerpc-methodb .
Sending build context to Docker daemon 13.31 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in bd3eda13f04f
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 132e6b06db8b
Removing intermediate container bd3eda13f04f
Step 3 : RUN echo "I'm powerpc"
 ---> Running in 6a46326d14ed
I'm powerpc
 ---> 827b8e6c3b6b
Removing intermediate container 6a46326d14ed
Step 4 : ADD overlay-common /overlay
 ---> 830fab32f246
Removing intermediate container 1b90a11e41e0
Step 5 : ADD overlay-powerpc /overlay
 ---> 4284b69e34cc
Removing intermediate container 73f13f124f71
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in a8c448044a67
 ---> 1d0dab2a9a57
Removing intermediate container a8c448044a67
Successfully built 1d0dab2a9a57
docker run --rm multiarch-dockerfile:powerpc-methodb uname -a
Linux af4fff98440d 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methodb ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methodb ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 17:41 .
drwxr-xr-x 34 root root 4096 Dec  7 17:41 ..
-rw-r--r--  1 root root    7 Dec  7 17:32 common
-rw-r--r--  1 root root    8 Dec  7 17:32 powerpc
```
