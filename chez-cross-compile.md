# download upstream source
git clone --depth 1 https://github.com/cisco/ChezScheme

build mingw target on win7 host
====

# patch
merge the contents of  patch-for-mingw directory.


msys>
 ./configure -m=ti3nt

Ϊ֧��windows xp, ta6nt/c/Makefile.i3nt �е� EXELDFLAGS �޸�Ϊ��
EXELDFLAGS=/machine:ix86 /incremental:no /release /nologo /STACK:0x800000 /SUBSYSTEM:CONSOLE,5.01

cmd>
 cd ta6nt\c
 .\make.bat


msys>

# update host boot to include modification from patch.
 (cd ta6nt; make -f Mf-boot ta6nt.boot)


# build target boot
 mkdir boot/ti3mw
 (cd ta6nt; make -f Mf-boot ti3mw.boot) #create new boot files
 

# build target with the target c compiler
./configure -m=ti3mw
make

build arm target on linux host
====


# build host
./configure
make


# build target boot
mkdir boot/arm32le
(cd a6le; make -f Mf-boot arm32le.boot)

# build target
./configure -m=arm32le CFLAGS="-O2 -march=armv7-a -mfpu=neon-vfpv4 -mfloat-abi=hard"
make

# ref
https://programmingpraxis.com/2017/09/15/compile-chez-scheme-on-android-arm/