---
layout: post
title: "first_run_gpgpu"
description: ""
category: "sphynx"
tags: [gpgpu, sphynx]
author: abagaria
---
{% include JB/setup %}


1. I followed the instructions from DH's blogs to setup git on my tera account. After that I cloned the GP-GPU sim files from the git repo into my tera account. 

2. I setup GP-GPU sim on my tera account. The README file in the v3.x directory was very helpful for this. As well as DH's blog. 

3. Then I tried to execute the make file. I got a LOT of warnings which did not go away on repeated builds, but I assumed that everything compiled properly.

3. At first I could not install Xming because I do not have root access. So if you get stuck in a similar situation, then ask DH to install it for you!

4. After that, we had to get get the SDK files and to make the programs in the SDK files. 

5. This was giving a lot of problems initially. This was because we were missing some library files which we did some searching online to understand how to acquire. For most of the library files, we ended up doing using yum install. 

6. After we got all the files, we were able to make successfully. 

7. However, we could not successfully make the example code on gp-gpu sim. This is the trace of the make command: 

```
[dhpark@tera ispass2009-benchmarks]$ make -f Makefile.ispass-2009
rm -f ../common; ln -s /home/dhpark/NVIDIA_GPU_Computing_SDK//C/common ..;
export BINDIR=/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispass2009-benchmar; export ROOTDIR=/home/dhpark/NVIDIA_GPU_Computing_SDK//src/; export BINSelease; export BOOST_LIB=/usr/lib64; export BOOST_ROOT=/usr/include; expoT_VER=""; export OPENMPI_BINDIR=/usr/lib64/mpi/gcc/openmpi/bin/;  make no0 -C AES
make[1]: Entering directory `/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispabenchmarks/AES'
sh: nvopencc: command not found
make[1]: *** [obj/release/aesHost.cu.o] Error 255
make[1]: Leaving directory `/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispasenchmarks/AES'
make: *** [default] Error 2
[dhpark@tera ispass2009-benchmarks]$
[dhpark@tera ispass2009-benchmarks]$ gedit ~/.bashrc
cannot open display:
Run 'gedit --help' to see a full list of available command line options.
[dhpark@tera ispass2009-benchmarks]$ gvim ~/.bashrc
E233: cannot open display
Press ENTER or type command to continue
[dhpark@tera ispass2009-benchmarks]$ ls
AES  bin  DG   LPS                   MUM  NQU  README.ISPASS-2009  STO
BFS  CP   LIB  Makefile.ispass-2009  NN   RAY  setup_config.sh     WP
[dhpark@tera ispass2009-benchmarks]$ make -f Makefile.ispass-2009
rm -f ../common; ln -s /home/dhpark/NVIDIA_GPU_Computing_SDK//C/common ..;
export BINDIR=/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispass2009-benchmar; export ROOTDIR=/home/dhpark/NVIDIA_GPU_Computing_SDK//src/; export BINSelease; export BOOST_LIB=/usr/lib64; export BOOST_ROOT=/usr/include; expoT_VER=""; export OPENMPI_BINDIR=/usr/lib64/mpi/gcc/openmpi/bin/;  make no0 -C AES
make[1]: Entering directory `/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispabenchmarks/AES'
sh: nvopencc: command not found
make[1]: *** [obj/release/aesHost.cu.o] Error 255
make[1]: Leaving directory `/home/dhpark/charlab/gpgpusim/gpgpu-sim/ispasenchmarks/AES'
make: *** [default] Error 2
```

8. We tried to edit the make file on vim to set the path so that it could find 'cutil.h' header file. I am not sure if we set the environment variable correctly in the make file. 

9. Despite my apprehensions about correctly setting the environment variable, it seemed like the compiler could find the file, it could not find a particular command. 

10. The error message is: 

		```
		sh: nvopencc: command not found
		make[1]: *** [obj/release/aesHost.cu.o] Error 255
		
		```

11. This nvopencc command should be (maybe?) in the SDK and toolkit files already. So I am not sure why it cannot find this command. 

12. We are so close to running our first program on GP-GPU Sim!


P.S: Here is the [link][jaja] which helped me understand the issue with the missing files while getting the SDK to compile: 
[jaja]: http://stackoverflow.com/questions/16024978/usr-bin-ld-cannot-find-lc-while-compiling-with-makefile

And here is the [Stack thread][thread] that we were following when we were (unsuccessfully) trying to run the example code on NVIDIA:
[thread]: http://stackoverflow.com/questions/12268373/compiling-basic-c-language-cuda-code-in-linux-ubuntu
