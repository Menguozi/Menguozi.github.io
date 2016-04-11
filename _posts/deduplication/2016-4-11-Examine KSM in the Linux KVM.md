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

>zuo@zuo:~$ egrep -o '(vmx|svm)' /proc/cpuinfo
>vmx
>vmx
>vmx
>vmx
>zuo@zuo:~$


#### 运行KSM


#### 主机配置
