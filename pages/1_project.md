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

## Path Hashing

* **A Write-friendly Hashing Scheme for Non-volatile Memory Systems**
* Emerging non-volatile memory technologies (NVMs) have been considered as promising candidates for replacing DRAM or SRAM, due to their advantages of high density, high scalability, and requiring no refresh power, while suffering from write performance and limited endurance. The significant changes of low-level memory devices cause nontrivial challenges to high-level in-memory or in-cache data structure design due to overlooking the NVM device properties. In this paper, we study an important and common data structure, hash table, which is ubiquitous and widely used to construct the index and lookup table in main memory and caches. Based on the observations that existing hashing schemes cause many extra writes to NVMs, we propose a cost-efficient write-friendly hashing scheme, called path hashing, which can significantly reduce extra writes for NVMs. The basic idea of path hashing is to leverage a novel hash-collision resolution method, i.e., position sharing, which meets the needs of insertion and deletion requests without extra writes to NVMs. By further exploiting double-path hashing and path shortening techniques, path hashing delivers high performance of hash tables in terms of space utilization and request latency. We have implemented path hashing and used  a GEM5 full system simulator with NVMain to evaluate its performance in the context of NVMs. Extensive experimental results demonstrate that path hashing incurs no extra writes to NVMs, and has high space utilization as well as low request latency, compared with existing state-of-the-art hashing schemes. We have released the source code of path hashing for public use at [Github](https://github.com/Pfzuo/Path-Hashing).

 

## BEES
* **BEES: Bandwidth- and Energy- Efficient Image Sharing for Real-time Situation Awareness**
* In order to save human lives and reduce injury and property loss, Situation Awareness (SA) information is essential and important for rescue workers to perform the effective and timely disaster relief. The information is generally derived from the shared images via widely used smartphones. However, conventional smartphone-based image sharing schemes fail to efficiently meet the needs of SA applications due to two main reasons, i.e., real-time transmission requirement and application-level image redundancy, which is exacerbated by limited bandwidth and energy availability. In order to provide efficient image sharing in disasters, we propose a bandwidth- and energy- efficient image sharing system, called BEES. The salient feature behind BEES is to propose the concept of Approximate Image Sharing (AIS), which explores and exploits approximate feature extraction, redundancy detection, and image uploading to trade the slightly low quality of computation results in content-based redundancy elimination for higher bandwidth and energy efficiency. Nevertheless, the boundaries of the tradeoffs between the quality of computation results and efficiency are generally subjective and qualitative. We hence propose the energy-aware adaptive schemes in AIS to leverage the physical energy availability to objectively and quantitatively determine the tradeoffs between the quality of computation results and efficiency. Moreover, unlike existing work only for out-of-batch similar images, BEES further eliminates in-batch ones via a similarity-aware submodular maximization model. We have implemented the BEES prototype which is evaluated via three real-world image datasets. Extensive experimental results demonstrate the efficacy and efficiency of BEES. We have released the source code of BEES for public use at [Github](https://github.com/Pfzuo/BEES).




**-- Some projects are not posted here due to their papers being reviewed in double-blind conferences.**
