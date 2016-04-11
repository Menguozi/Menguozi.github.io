---
layout: post
Title: Examine KSM in the Linux KVM
comments: true
categories: KSM Deduplication KVM

---

#### 安装KVM
1 首先查看主机CPU的虚拟化支持
        
`$ egrep -o '(vmx|svm)' /proc/cpuinfo`

如果显示如下则表示该主机CPU支持虚拟化

> zuo@zuo:~$ egrep -o '(vmx|svm)' /proc/cpuinfo   
vmx   
vmx   
vmx   
vmx   
zuo@zuo:~$   

2 安装KVM软件包：virt-manager为GUI管理窗口，bridge-utils:用于网络桥接

`$ apt-get install qemu-kvm libvirt-bin virt-manager bridge-utils`

3. 检查KVM是否安装成功
    方法1：
    
    `$ lsmod | grep kvm`
    
    如果显示如下信息，则表示KVM安装成功
    
    > zuo@zuo:~$ lsmod | grep kvm   
      kvm_intel             143630  0    
      kvm                   452096  1 kvm_intel   
      zuo@zuo:~$    
    
    方法2：
    
    `$ virsh -c qemu:///system list`
    
    如果显示如下信息，则表示KVM安装成功
    
    > zuo@zuo:~$ virsh -c qemu:///system list   
        Id    Name                           State   
        ----------------------------------------------------   
            
        zuo@zuo:~$    

    

#### 运行KSM


#### 主机配置
