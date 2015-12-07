# dockerfile
Multiarch Dockerfile POC

---

                                               | A | B | C | D | E | F | G
-----------------------------------------------|---|---|---|---|---|---|---
Unique Dockerfile                              | x |   | x |   | x | x | x
Complete multiarch support                     | x | x |   |   | x |   | x
Does not require a Makefile for amd64          |   |   | x |   | x | x | x
Gentle multiline support                       |   |   |   |   |   | x | x
Dockerfile is easily readable                  |   | x | x |   | x | x | x
Disk-friendly (do not create tmp context dir)  | x | x |   |   |   | x |
