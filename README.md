## Instructions for opening the vm
1) ssh into attu
2) navigate to the folder that contains the vm image
3) run the practice.sh script
4) __chmod +x practice.sh__ (only if you don't already have practice.sh set to executable)
5) __./practice.sh__
6) open a new terminal and ssh into the same attu server
7) __ssh -p 6500 suneja@127.0.0.1__
8) __password: suneja__

I mostly used this blog to complete this assignment: https://blog.sourcerer.io/writing-a-simple-linux-kernel-module-d9dc3762c234 

## Instructions for installing headers
1) __sudo sh__ #to get to the root
2) __apt-get install build-essential linux-headers-'uname -r'__
3) __exit__ #once everything has finished installing

## Instructions for creating a kernel module
1)	__mkdir akhila-assignment__
2)	copy __hello_world.c__ and __Makefile__ into this folder
3)	__make__ #run make
4)	__sudo insmod hello_world.ko__ #insert the module
5)	__sudo dmesg__ #opens kernel log, should see Hello World at the bottom
6)	__sudo rmmod hello_world__ #removes module
7)	__sudo dmesg__ #opens kernel log, should see Goodbye! at the bottom

## Things that went wrong and how I fixed them
### Problem 1:

The first time I tried running __apt-get install build-essential linux-headers-'uname -r'__, I got an error saying:

  E: Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 4772 (unattended-upgr)<br>
	N: Be aware that removing the lock file is not a solution and may break your system.<br>
  E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?<br>
  
This is how I resolved it:  
1) __ps -eaux__ #to find the process 4772
2) __ps -eax | grep 4772__ #to see what the process is, it is an old python script
3) __kill -9 4772__
4) __apt-get install build-essential linux-headers-'uname -r'__ #run this again 

### Problem 2:
I copied my __hello_world.c__ and __Makfile__ code from the internet, so I had some formatting errors. 

I found my __Makefile__ errors by doing a dry run, __make -n__, and googled the errors I received (just some indenting problems).

To find my __hello_world.c__ errors I ran __make > errors.txt 2>&1__ to easily view all the errors in a single file. Turns out the code I copied used ASCII quotation marks instead of Unicode. 
