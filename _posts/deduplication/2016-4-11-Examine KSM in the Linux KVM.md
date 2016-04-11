---
layout: post
Title: Examine KSM in the Linux KVM
comments: true
categories: KSM Deduplication KVM

---

### 安装KVM
---


1. 首先查看主机CPU的虚拟化支持:
        
    `$ egrep -o '(vmx|svm)' /proc/cpuinfo`

    如果显示如下,则表示该主机CPU支持虚拟化

        zuo@zuo:~$ egrep -o '(vmx|svm)' /proc/cpuinfo   
        vmx   
        vmx   
        vmx   
        vmx   
        zuo@zuo:~$   

2. 安装KVM软件包：virt-manager为GUI管理窗口，bridge-utils:用于网络桥接

    `$ apt-get install qemu-kvm libvirt-bin virt-manager bridge-utils`

3. 检查KVM是否安装成功

    方法1：
    
    `$ lsmod | grep kvm`
    
    如果显示如下信息，则表示KVM安装成功
    
        zuo@zuo:~$ lsmod | grep kvm   
        kvm_intel             143630  0    
        kvm                   452096  1 kvm_intel   
        zuo@zuo:~$    
    
    方法2：
    
    `$ virsh -c qemu:///system list`
    
    如果显示如下信息，则表示KVM安装成功
    
        zuo@zuo:~$ virsh -c qemu:///system list   
        Id    Name                           State   
        ----------------------------------------------------   
        zuo@zuo:~$    

4. 比较容易被忽视的一点是：开机前，进入BIOS中，开启CPU虚拟化支持

        Intel(R) Virtualization Technology (Enabled)
 
### 运行KVM
---

1. 终端中输入如下指令，打开virtual machine manager

    `$ sudo virt-manager`

   这时会弹出virtual machine manager的界面
     
2. 创建虚拟机前，需要下载一个操作系统的镜像文件（.iso）,用于安装虚拟机的操作系统;   
   点击virtual machine manager界面上的“create a new virtual machine”按钮，就可以开始创建虚拟机了（如下图所示）:
   
   ![image](https://pfzuo.github.io/images/createVM.png)


### 运行KSM
---

1. KSM需要在root权限下运行，所以首先获取root权限：

    `# su root`
    
        zuo@zuo:~$ su root   
        Password:   
        root@zuo:/home/zuo#    

2. KSM进程由'/sys/kernel/mm/ksm/'路径中的文件控制，我们可以查看KSM的运行状态：
    
    `# grep -H '' /sys/kernel/mm/ksm/*`
    
    结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:0
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:0
        /sys/kernel/mm/ksm/pages_sharing:0
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:0
        /sys/kernel/mm/ksm/pages_volatile:0
        /sys/kernel/mm/ksm/run:0
        /sys/kernel/mm/ksm/sleep_millisecs:200
        root@zuo:/home/zuo# 
     
     其中每个参数的含义可参照 [https://www.kernel.org/doc/Documentation/vm/ksm.txt](https://www.kernel.org/doc/Documentation/vm/ksm.txt)

3. 开启KSM进程：
    
    `# echo 1 > /sys/kernel/mm/ksm/run`
    

### 虚拟机内存去重的性能测试
---

1. 我首先用KVM创建了3个相同的Linux虚拟机(系统：Ubuntu-12.04 32位, 内存：1GB，硬盘空间：8GB);

2. 只开启一个虚拟机，查看内存去重情况

    ![image](https://pfzuo.github.io/images/oneVM.png)
    
    KSM开始合并相同内存页，约12分钟后，内存相对稳定，内存去重结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*   
        /sys/kernel/mm/ksm/full_scans:3   
        /sys/kernel/mm/ksm/merge_across_nodes:1   
        /sys/kernel/mm/ksm/pages_shared:11808   
        /sys/kernel/mm/ksm/pages_sharing:40450   
        /sys/kernel/mm/ksm/pages_to_scan:100  
        /sys/kernel/mm/ksm/pages_unshared:115310   
        /sys/kernel/mm/ksm/pages_volatile:2526   
        /sys/kernel/mm/ksm/run:1   
        /sys/kernel/mm/ksm/sleep_millisecs:200   


3. 同时开启两个虚拟机，查看内存去重情况

    ![image](https://pfzuo.github.io/images/twoVMs.png)
    
    约20分钟后（3次full scan），内存去重结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:6
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:21481
        /sys/kernel/mm/ksm/pages_sharing:98382
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:209164
        /sys/kernel/mm/ksm/pages_volatile:16901
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
        
    约35分钟后(4次full scan)，内存相对稳定，内存去重结果如下：
    
        root@zuo:/home/zuo# grep -H '' /sys/kernel/mm/ksm/*
        /sys/kernel/mm/ksm/full_scans:7
        /sys/kernel/mm/ksm/merge_across_nodes:1
        /sys/kernel/mm/ksm/pages_shared:82113
        /sys/kernel/mm/ksm/pages_sharing:162811
        /sys/kernel/mm/ksm/pages_to_scan:100
        /sys/kernel/mm/ksm/pages_unshared:95096
        /sys/kernel/mm/ksm/pages_volatile:5908
        /sys/kernel/mm/ksm/run:1
        /sys/kernel/mm/ksm/sleep_millisecs:200
    
    
4. 同时开启三个虚拟机，查看内存去重情况

    ![image](https://pfzuo.github.io/images/threeVMs.png)


    KSM进程的CPU占用一直处于0.3%～0.7%间;









