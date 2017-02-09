---
layout: page
title: Project
comments: true
permalink: /project/
---

* content
{:toc}

# My Projects
---
## DeWrite 

* **Enhancing Lifetime and Performance of Secure Non-Volatile Memory Systems through Eliminating Duplicate Writes**
* Non-volatile memory (NVM) technologies are considered as promising candidates for replacing DRAM. However, the non-volatility of NVMs leads to new security vulnerabilities. For example, it is not difficult to access sensitive data stored on stolen NVMs. Memory encryption can be employed to mitigate the security vulnerabilities, but it increases the number of bits written to NVMs due to the diffusion property and thereby aggravates the NVM wear-out induced by writes. To address these security and endurance challenges, this paper proposes a novel secure and deduplication-aware scheme, DeWrite, with new in-line deduplication and encryption techniques and the synergistic integration of the two. Specifically, it performs low-latency in-line deduplication by using light-weight hashing, instead of commonly used cryptographic hashing, and leveraging the intrinsic read/write asymmetry of NVMs. It also parallelizes the operations of deduplication and encryption and allows them to share the metadata for high time and space efficiency. Dewrite was implemented on a GEM5 full system simulator and evaluated using 24 applications from SPEC CPU 2006 and PARSEC benchmark suites. Extensive experimental results demonstrate that DeWrite reduces 55% writes to secure NVMs, and speeds up memory writes (reads) by 3.7 times 2.9 times. Meanwhile, DeWrite improves 67% IPC and reduces 34% energy overhead on average.


## RRCS 

* **A Bandwidth-efficient Scheme for Mitigating the Side Channel Attacks in Cloud Storage Services**
* Deduplication is able to effectively identify and eliminate redundant data and only maintain a single copy of files and chunks. Hence, it is widely used in cloud storage systems to save storage space and network bandwidth. However, the occurrence of deduplication can be easily identified by monitoring and analyzing network traffic, which leads to the risk of users' privacy leakage. Deduplication can be used as a side channel to reveal privacy information of users. In order to address this problem, we propose an easy-to-use and bandwidth-efficient scheme, called randomized redundant chunk scheme (RRCS), to mitigate the risk of side channel attacks while maintaining the high bandwidth efficiency of deduplication. By carefully adding randomly chosen redundant chunks for each uploaded file, RRCS can mix up the real deduplication states of files and effectively obfuscate the view of the attacker, who attempts to exploit the amount of the transmitted data for side channel attacks. Our security analysis shows that RRCS could significantly mitigate the risk of the side channel attacks. We implement the RRCS prototype and evaluate it by using three large-scale real-world datasets. Experimental results demonstrate that RRCS delivers high performance while providing security guarantee.
 

## BEES
* **BEES: Bandwidth- and Energy- Efficient Image Sharing for Real-time Situation Awareness**
* In order to save human lives and reduce injury and property loss, Situation Awareness (SA) information is essential and important for rescue workers to perform the effective and timely disaster relief. The information is generally derived from the shared images via widely used smartphones. However, conventional smartphone-based image sharing schemes fail to efficiently meet the needs of SA applications due to two main reasons, i.e., real-time transmission requirement and application-level image redundancy, which is exacerbated by limited bandwidth and energy availability. In order to provide efficient image sharing in disasters, we propose a bandwidth- and energy- efficient image sharing system, called BEES. The salient feature behind BEES is to propose the concept of Approximate Image Sharing (AIS), which explores and exploits approximate feature extraction, redundancy detection, and image uploading to trade the slightly low quality of computation results in content-based redundancy elimination for higher bandwidth and energy efficiency. Nevertheless, the boundaries of the tradeoffs between the quality of computation results and efficiency are generally subjective and qualitative. We hence propose the energy-aware adaptive schemes in AIS to leverage the physical energy availability to objectively and quantitatively determine the tradeoffs between the quality of computation results and efficiency. Moreover, unlike existing work only for out-of-batch similar images, BEES further eliminates in-batch ones via a similarity-aware submodular maximization model. We have implemented the BEES prototype which is evaluated via three real-world image datasets. Extensive experimental results demonstrate the efficacy and efficiency of BEES. We have released the source code of BEES for public use at [Github](https://github.com/Pfzuo/BEES).



