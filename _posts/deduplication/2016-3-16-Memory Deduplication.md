---
layout: post
comments: true
categories: Deduplication KSM

---

#### Memory Deduplication
>Memory deduplication aims to save memory space in RAM by identifying and merging the identical memory pages. Red Hat proposed the KSM (Kernel Shared Memory or Kernel Same-page Merging)[^KSM] technique to implement memory deduplication in Linux kernel. KSM has merged into Linux kernel since the version 2.6.32 in 2009[^Linux2632]. VMware also proposed a technique called TPS (Transparent Page Sharing)[^TPS] in its product ESXi for memory deduplication. Some literatures claims that KSM may be more efficient than TPS. However, I have not seen any work comparing them in real experiments.


#### KSM (Kernel Shared Memory or Kernel Same-page Merging)

> KSM leverages two red-black trees to manage the memory pages, i.e., a stable tree and a unstable tree.

#### TPS (Transparent Page Sharing)

> TPS uses the hash value of memory page's content to identify the same page.


To be continued ......

----

### References:

[^KSM]: Arcangeli A, Eidus I, Wright C. *Increasing memory density by using KSM*. In proceedings of the Linux ymposium. 2009.
[^Linux2632]: *Linux kernel 2.6.32, Section 1.3. Kernel Samepage Merging (memory deduplication)*. [kernelnewbies.org][kernel]. 2009.
[^TPS]: Guo F. *Understanding memory resource management in vmware vsphere 5.0*. VMware Inc, 2011.

[kernel]: http:\\kernelnewbies.org\