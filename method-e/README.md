```console
root@fwrz:~/dockerfile/method-e# make TARGET=powerpc
docker build --no-cache -t multiarch-dockerfile:powerpc-methode tmp-powerpc
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:powerpc-wily
 ---> 6c3238952754
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 1a2f37e8f2b5
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> 9bb484d3dfed
Removing intermediate container 1a2f37e8f2b5
Step 3 : RUN echo "I'm powerpc"
 ---> Running in 5acf39b9da6b
I'm powerpc
 ---> 350bd01dc34d
Removing intermediate container 5acf39b9da6b
Step 4 : ADD overlay-common /overlay
 ---> ea6f628eac5c
Removing intermediate container a20b10a0b399
Step 5 : ADD overlay-powerpc /overlay
 ---> 60362e31754f
Removing intermediate container ee4e6484b525
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in d6ad695847aa
 ---> 6f758d35065d
Removing intermediate container d6ad695847aa
Successfully built 6f758d35065d
docker run --rm multiarch-dockerfile:powerpc-methode uname -a
Linux 30e2dd7ac3cb 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 ppc ppc ppc GNU/Linux
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 481776 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:powerpc-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 18:13 .
drwxr-xr-x 34 root root 4096 Dec  7 18:13 ..
-rw-r--r--  1 root root    7 Dec  7 18:12 common
-rw-r--r--  1 root root    8 Dec  7 18:12 powerpc
```

```console
root@fwrz:~/dockerfile/method-e# make TARGET=amd64
docker build --no-cache -t multiarch-dockerfile:amd64-methode tmp-amd64
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> 0fdd22782955
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in 39b4c4f04142
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.9 kB]
Fetched 2371 kB in 2s (803 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> d95c4d8cb401
Removing intermediate container 39b4c4f04142
Step 3 : RUN echo "I'm amd64"
 ---> Running in 6f692e30b8ea
I'm amd64
 ---> a441f20535ce
Removing intermediate container 6f692e30b8ea
Step 4 : ADD overlay-common /overlay
 ---> 99ef90b38e25
Removing intermediate container 5859e5f5a98a
Step 5 : ADD overlay-amd64 /overlay
 ---> 737c67db1b05
Removing intermediate container 5be623b9bc0b
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 37cb71325694
 ---> 2e362ce51120
Removing intermediate container 37cb71325694
Successfully built 2e362ce51120
docker run --rm multiarch-dockerfile:amd64-methode uname -a
Linux 0948382423c4 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 18:14 .
drwxr-xr-x 36 root root 4096 Dec  7 18:14 ..
-rw-r--r--  1 root root    6 Dec  7 18:12 amd64
-rw-r--r--  1 root root    7 Dec  7 18:12 common
```

```console
root@fwrz:~/dockerfile/method-e# make TARGET=armhf
docker build --no-cache -t multiarch-dockerfile:armhf-methode tmp-armhf
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:armhf-wily
 ---> aeed111b7935
Step 2 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in a62451ee370e
Reading package lists...
Reading package lists...
Building dependency tree...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
 ---> cfcfd5e10d47
Removing intermediate container a62451ee370e
Step 3 : RUN echo "I'm arhmf"
 ---> Running in 3f55f07332cc
I'm arhmf
 ---> 82ba3395a7a0
Removing intermediate container 3f55f07332cc
Step 4 : ADD overlay-common /overlay
 ---> 32123b3c5676
Removing intermediate container 4fc4516ee59a
Step 5 : ADD overlay-armhf /overlay
 ---> 857eb60044bb
Removing intermediate container a2fb3806b864
Step 6 : CMD uname -a; cowsay hello world
 ---> Running in 8aa2464c294e
 ---> 24d7d8038f08
Removing intermediate container 8aa2464c294e
Successfully built 24d7d8038f08
docker run --rm multiarch-dockerfile:armhf-methode uname -a
Linux c30131858027 3.13.0-36-generic #63-Ubuntu SMP Wed Sep 3 21:30:07 UTC 2014 armv7l armv7l armv7l GNU/Linux
docker run --rm multiarch-dockerfile:armhf-methode ls -la /usr/bin/wget
-rwxr-xr-x 1 root root 330100 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:armhf-methode ls -la /overlay
total 16
drwxr-xr-x  2 root root 4096 Dec  7 18:14 .
drwxr-xr-x 34 root root 4096 Dec  7 18:14 ..
-rw-r--r--  1 root root    6 Dec  7 18:12 armhf
-rw-r--r--  1 root root    7 Dec  7 18:12 common
```
