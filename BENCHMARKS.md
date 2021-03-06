## Intro

Some people have expressed opinions about how fast libb64's encoding and decoding routines are, as compared to some other BASE64 packages out there.

This document shows the result of a short and sweet benchmark, which takes a large-ish file and encodes/decodes it a number of times.
The winner is the executable that does this task the quickest.

## Platform

The tests were all run on a Fujitsu-Siemens laptop, with a Pentium M processor running at 2 GHz, with 1 GB of RAM, running Ubuntu 10.4.

## Packages

The following BASE64 packages were used in this benchmark:

- libb64-1.2 (libb64-base64)
  From libb64.sourceforge.net
  Size of executable: 18808 bytes
  Compiled with:
    CFLAGS += -O3
    BUFFERSIZE = 16777216

- base64-1.5 (fourmilab-base64)
  From http://www.fourmilab.ch/webtools/base64/
  Size of executable: 20261 bytes
  Compiled with Default package settings

- coreutils 7.4-2ubuntu2 (coreutils-base64)
  From http://www.gnu.org/software/coreutils/
  Size of executable: 38488 bytes
  Default binary distributed with Ubuntu 10.4

## Input File

Using `blender-2.49b-linux-glibc236-py25-i386.tar.bz2` from http://www.blender.org/download/get-blender/
Size: 18285329 bytes (approx. 18 MB)

## Method

Encode and Decode the Input file 50 times in a loop, using a simple shell script, and get the running time.

## Results

    $ time ./benchmark-libb64.sh
    real    0m28.389s
    user    0m14.077s
    sys     0m12.309s

    $ time ./benchmark-fourmilab.sh
    real    1m43.160s
    user    1m23.769s
    sys     0m8.737s

    $ time ./benchmark-coreutils.sh
    real    0m36.288s
    user    0m24.746s
    sys     0m8.181s

    28.389 for 18 MB * 50
    = 28.389 for 900 MB

## Conclusion

libb64 is the fastest encoder/decoder, and has the smallest executable size.

On average it will encode and decode at roughly 31.7 MB/second.

The closest "competitor" is base64 from GNU coreutils, which reaches only 24.8 MB/second.

--
14/06/2010
chris.venter@gmail.com
