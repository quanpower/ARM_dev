拿到一个RK3288的开发板，但是不得不说adb shell不太好用，像下面这样太锉了。
![在此输入图片描述][1]

于是想着把busybox编译进去。

# 1.  准备编译环境

其实现在Ubuntu上交叉编译相比之前要简单那很多。


## 1.1 安装 JDK 6：
    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java6-installer


## 1.2 依赖包：
Ubuntu 12.04 软件包安装：

    sudo apt-get install git gnupg flex bison gperf build-essential \
     zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
     libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
     g++-multilib mingw32 tofrodos gcc-multilib ia32-libs\
     python-markdown libxml2-utils xsltproc zlib1g-dev:i386

Ubuntu 13.10/14.04 软件包安装：

    sudo apt-get install git-core gnupg flex bison gperf libsdl1.2-dev \
     libesd0-dev libwxgtk2.8-dev squashfs-tools build-essential zip curl \
     libncurses5-dev zlib1g-dev pngcrush schedtool libxml2 libxml2-utils \
     xsltproc lzop libc6-dev schedtool g++-multilib lib32z1-dev lib32ncurses5-dev \
     lib32readline-gplv2-dev gcc-multilib libswitch-perl

## 1.3 安装 ARM 交叉编译工具链和编译内核相关软件包：

    sudo apt-get install gcc-arm-linux-gnueabihf \
     lzop libncurses5-dev \
     libssl1.0.0 libssl-dev

这里至于gcc-arm-linux-gnueabihf还是gcc-arm-linux-gnueabi要看你芯片，应该是hard float吧

# 2.busybox源代码

下载最新版本busybox源码，下载地址：http://www.busybox.net/downloads/。

    $ mkdir ~/busybox                      # 创建工作目录
    $ cp busybox-1.22.1.tar.bz2 ~/busybox  # 复制源码包
    $ cd ~/busybox/                        # 进入工作目录
    $ tar -jxvf busybox-1.22.1.tar.bz2     # 解压
    $ cd busybox-1.22.1/                   # 进入解压包

# 3.编译准备

## 3.1 环境变量
    dpkg -L gcc-arm-linux-gnueabihf
看装哪里了，apt-get安装的还好，一般都/usr/bin了，没有的要加到环境变量

## 3.2 建立安装文件夹
    mkdir busybox-install

# 4. meke menuconfig

根据个人喜好，用menuconfig或者直接修改.config,主要是这里有几点注意：

## 4.1 选择交叉编译器前缀
这里是前缀，不加gcc,到-结束，如我的：arm-linux-gnueabihf-；
    Busybox Settings --> Build Options --> Cross compiler prefix  -  Set this option equal to "arm-linux-gnueabihf-"；

## 4.2 静态编译
建议使用静态编译；
    Busybox Settings --> Build Options --> Build Busybox as a static binary (no shared libs)  -  Enable this option by pressing "Y"
![在此输入图片描述][2]

## 4.3  不包含/usr目录
 Busybox Settings --> Installation Options --> Don't use /usr  -  Enable this option by pressing "Y"
![在此输入图片描述][3]

## 4.4 安装目录
上一步的install目录，要使用绝对路径。
![在此输入图片描述][4]

## 4.5 最后按【ESC】，提示保存时保存。

# 5. make && make install

    $ make                                  # 编译，如果是多核CPU，如四核，使用make -j4可提高编译速度
    $ make install                          # 安装


# 6. 发送

或用Root Explore 把/挂载为可读写

    adb shell mkdir busybox
    
    adb push ./bin /busybox/bin
    adb push ./sbin /busybox/sbin
    
    export PATH=/busybox/bin:/busybox/sbin:$PATH:

# 7. 完结。

看下效果，跟前面adb shell是不是天壤之别了。如果再配合安装个SSH SERVER用就更爽了，完全脱离adb，主要是有VI 了，可以远程键盘编辑了。
![在此输入图片描述][5]


  [1]: http://static.oschina.net/uploads/space/2014/1213/025853_uIyJ_438461.jpg
  [2]: http://static.oschina.net/uploads/space/2014/1213/020418_Ujtu_438461.jpg
  [3]: http://static.oschina.net/uploads/space/2014/1213/020443_zwSx_438461.jpg
  [4]: http://static.oschina.net/uploads/space/2014/1213/020502_5WQG_438461.jpg
  [5]: http://static.oschina.net/uploads/space/2014/1213/021812_tEkq_438461.jpg
