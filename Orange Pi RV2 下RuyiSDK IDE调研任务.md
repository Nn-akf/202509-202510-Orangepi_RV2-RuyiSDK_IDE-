# Orange Pi RV2 下RuyiSDK IDE调研任务

## 开发板：Orange Pi RV2

### 镜像：Orangepirv2_1.0.0_ubuntu_noble_desktop_gnome_lin。

## 虚拟机环境：Ubuntu22.04

## 1.交叉编译

​	在虚拟机上构建RISC-V架构的开发环境是进行orangepiRV2开发必不可少的一步，参考官方给出的用户手册，步骤大致可分为以下几点：

### 	1.获取源码：

```
sudo apt-get update	#软件源等的更新
sudo apt-get install -y git #进行git的下载
git clone https://github.com/orangepi-xunlong/orangepi-build.git -b next #从github上下载Orangepi-build的下载
```

​	***难点***：在官网给出的示例中，从用户实际操作的角度出发，在进行前两步的更新和下载操作时可能不会出现难以解决的问题。但是在进行第三步骤从github上拉取orangepi-build时，由于代理和和网络服务商限制的问题，大概率会出现连接超时的问题。这时一般来说，最好的办法是在windows下使用代理，下载在windows中，后经过Filezilla或“share”文件夹传递到Ubuntu下。

### 	2.下载交叉编译工具链

​	官方手册里推荐在清华大学开源软件镜像站中进行下载

```
https://mirrors.tuna.tsinghua.edu.cn/armbian-releases/_toolchain/
```

​	但是我在此网站下并没有找到相应的工具链“riscv64-unknown-linux-gnu-gcc”与“riscv64-unknown-linux-gnu-gcc”（有可能已经不支持了，2025.9.29），若想使用工具链须从官方打包的工具链中进行下载。

### 	编译u-boot、内核、rootfs

​	首先进入到orangepi-build目录下，运行“sudo ./build.sh”，运行脚本并选择相应的型号。其中三个过程都比较的占用时间和内存，且在运行结束之后需要把编译好的相应的文件上传到开发板中进行重新的配置。

​	***难点***：编译内核、u-boot是一个占用时间和内存很大的过程，如果在RuyiSDK IDE的终端下运行，软件是否能够可以进行承载相应的内存和处理压力。且如果是在IDE中进行相应的内核等的编译，在进行相应的参数选择时，终端是否可以支持图形化界面进行具象化的参数选择。其次，编译成功的文件需上传到开发板并进行权限等配置，IDE是否可以进行SSH连接相应的开发板，进行文件的上传，这样可以为用户的操作提供便利性，提升用户体验的同时增加IDE的兼容性。

​	