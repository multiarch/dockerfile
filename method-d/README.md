````docker build --no-cache -t multiarch-dockerfile:amd64-methode tmp-amd64
Sending build context to Docker daemon  5.12 kB
Step 1 : FROM multiarch/ubuntu-debootstrap:amd64-wily
 ---> b5f39c8c167e
Step 2 : ARG ARCH
 ---> Running in be897279dc64
 ---> 3477505d21ba
Removing intermediate container be897279dc64
Step 3 : RUN apt-get update && apt-get install --no-install-recommends -y -q wget
 ---> Running in e2240b74d258
Get:1 http://archive.ubuntu.com wily InRelease [218 kB]
Get:2 http://archive.ubuntu.com wily-updates InRelease [64.4 kB]
Get:3 http://archive.ubuntu.com wily-security InRelease [64.4 kB]
Get:4 http://archive.ubuntu.com wily/main amd64 Packages [1833 kB]
Get:5 http://archive.ubuntu.com wily-updates/main amd64 Packages [117 kB]
Get:6 http://archive.ubuntu.com wily-security/main amd64 Packages [74.9 kB]
Fetched 2371 kB in 1s (1585 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
wget is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
 ---> 9914562f4006
Removing intermediate container e2240b74d258
Step 4 : RUN [ "${ARCH}" = "amd64" ] || echo "Special build instruction for amd64"
 ---> Running in 13e85c7c13a5
Special build instruction for amd64
 ---> da8fb4c8ad98
Removing intermediate container 13e85c7c13a5
Step 5 : ADD overlay-common /overlay
 ---> 465dd0455c94
Removing intermediate container fa44fb36def4
Step 6 : ADD overlay-amd64 /overlay
 ---> 70d10609b712
Removing intermediate container ac5fc0eddfcb
Step 7 : CMD uname -a; cowsay hello world
 ---> Running in 41670bd10f84
 ---> 37602ccf0e43
Removing intermediate container 41670bd10f84
Successfully built 37602ccf0e43
docker run --rm multiarch-dockerfile:amd64-methode uname -a
Linux 2bf596e00437 4.2.5-1-ARCH #1 SMP PREEMPT Tue Oct 27 08:13:28 CET 2015 x86_64 x86_64 x86_64 GNU/Linux
docker run --rm multiarch-dockerfile:amd64-methode ls -la /usr/bin/wget
-rwxr-xr-x 33 root root 454176 Jan 13  2015 /usr/bin/wget
docker run --rm multiarch-dockerfile:amd64-methode ls -la /overlay
total 16
drwxr-xr-x 2 root root 4096 Dec  7 18:40 .
drwxr-xr-x 1 root root 4096 Dec  7 18:40 ..
-rw-r--r-- 2 root root    6 Dec  7 18:39 amd64
-rw-r--r-- 3 root root    7 Dec  7 18:39 common
```
