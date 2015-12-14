# dockerfile
Multiarch Dockerfile POC

---

**Update**: method G is now successfully implemented here: https://github.com/scaleway/image-ubuntu/tree/master/15.10, we now hope the method H to be possible soon, so we can switch again

---

                                               | A | B | C | D | E | F | G | H
-----------------------------------------------|---|---|---|---|---|---|---|---
Unique Dockerfile                              | x |   | x |   | x | x | x | x
Complete multiarch support                     | x | x |   |   | x |   | x | x
Does not require a Makefile for amd64          |   |   | x |   | x | x | x | x
Gentle multiline support                       |   |   |   |   |   | x | x | x
Dockerfile is easily readable                  |   | x | x |   | x | x | x | x
Disk-friendly (do not create tmp context dir)  | x | x |   |   |   | x |   | x
Does not need to patch Docker                  | x | x | x | x | x |   | x |
                                               |   |   |   |   |   |   |   |
*Votes*                                        |   |   |   |   |0.5|   |1.5| 3

---

Vote scoring (per person):
* First choice: 1 vote
* Secondary choice(s): 0.5 vote 
