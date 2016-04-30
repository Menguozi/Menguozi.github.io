---
layout: post
comments: true
categories: GEM5

---

GEM5是一个非常强大的服务于计算机系统架构研究的模拟平台，包括系统级架构和处理器微架构。最近在做GEM5相关的研究工作，顺便在blog上记下学习笔记。本文主要怎么正确地在Linux系统上安装和运行GEM5。

> ## 安装一些依赖软件
---

运行GEM5需要一些依赖软件，包括：g++ （4.7版本及以上）、Python （2.5版本及以上）、 SCons （0.98.1版本及以上）、 SWIG （2.0.4版本及以上）、zlib、m4、 protobuf （2.1版本及以上）。

### 1. 安装g++

g++一般系统自带，可用 `g++ -v` 查看版本号。

如果系统没有的话，使用如下命令安装：

    sudo apt-get install g++

### 2. 安装Python

Python一般系统自带，可用 `python --version` 查看版本号。

### 3. 安装Scons

使用以下命令安装SCons：
       
    sudo apt-get install scons
     
安装后查看版本号：

    scons -v

### 4. 安装SWIG

[SWIG下载地址] (http://swig.org/)，解压后安装：

    ./configure   
    make    
    sudo make install   
        
安装后查看版本号：

    swig -version
        
### 5. 安装zlib
zlib一般系统自带，使用 `whereis zlib` 查看安装位置，如果系统没有的话，使用如下步骤安装：

[zlib下载地址] (http://www.zlib.net/)，解压后安装：

    ./configure   
    make    
    sudo make install   
        
### 6. 安装m4

一般系统自带，使用 `m4 --veriosn` 查看版本，如果系统没有的话，使用如下步骤安装：

[m4下载地址] （http://www.gnu.org/software/m4/m4.html），解压后安装：

    ./configure   
    make    
    sudo make install  

### 7. 安装protobuf

[protobuf下载地址] （https://github.com/google/protobuf）， 解压后安装：

    ./configure   
    make    
    sudo make install  
        
然后使用如下命令可以查看版本号，检查是否安装完成：

    protoc --version 

### 8. 安装 libprotobuf-dev 和 libgoogle-perftools-dev

    sudo apt-get install libprotobuf-dev    
    sudo apt-get install libgoogle-perftools-dev   


> ## 运行GEM5
---

### 1. 下载GEM5

[GEM5稳定版下载地址] (http://repo.gem5.org/gem5-stable)， 然后解压。

### 2. 编译GEM5

以编译一个RAM处理器为例：

    scons build/ARM/gem5.opt
        
### 3. 测试

大约十几分钟后，编译完成，输入如下命令进行测试：

    ./build/ARM/gem5.opt ./configs/example/se.py -c ./tests/test-progs/hello/bin/arm/linux/hello
        
运行结果如下：
        
    root@zuo:/home/zuo/GEM5/gem5-stable# ./build/ARM/gem5.opt ./configs/example/se.py -c ./tests/test-progs/hello/bin/arm/linux/hello
    gem5 Simulator System.  http://gem5.org
    gem5 is copyrighted software; use the --copyright option for details.

    gem5 compiled May  1 2016 00:37:35
    gem5 started May  1 2016 00:51:06
    gem5 executing on zuo
    command line: ./build/ARM/gem5.opt ./configs/example/se.py -c ./tests/test-progs/hello/bin/arm/linux/hello

    /home/zuo/GEM5/gem5-stable/configs/common/CacheConfig.py:48: SyntaxWarning: import * only allowed at module level
    def config_cache(options, system):
    Global frequency set at 1000000000000 ticks per second
    warn: DRAM device capacity (8192 Mbytes) does not match the address range assigned (512 Mbytes)
    0: system.remote_gdb.listener: listening for remote gdb #0 on port 7000
    **** REAL SIMULATION ****
    info: Entering event queue @ 0.  Starting simulation...
    Hello world!
    Exiting @ tick 2924500 because target called exit()
    root@zuo:/home/zuo/GEM5/gem5-stable# 

可见输出来有Hello world!表示运行成功。

        


