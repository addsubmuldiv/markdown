# ICWS2021论文

## Microservice Pre-deployment Based on Mobility Prediction and Service Composition in Edge

文章主要内容是   解决移动用户在MEC环境下请求服务可能失败的问题，通过集成移动预测和服务组合的微服务预部署方法。



之前打算用强化学习解决这个问题，可以借鉴建模和大致需要考虑的问题



## User Allocation in Mobile Edge Computing: A Deep Reinforcement Learning Approach

我们提供了一个设备上深度强化学习 (DRL) 框架来预测来自用户的传入服务请求的资源利用率，从而估计边缘服务器可以容纳给定延迟阈值的用户数量。



强化学习、和现在在搞的有点像



## An Efficient Algorithm for Service Function Chains Reconfiguration in Mobile Edge Cloud Networks

网络功能虚拟化 (NFV) 与 MEC 技术一起，在 MEC 服务器上提供服务功能链 (SFC)，以改善用户服务体验并实现对移动用户的快速访问。 但是，用户在边缘网络中不断移动，不同的用户通常对服务请求有不同的延迟要求。 为保证移动用户的QoS，当用户跨基站（BS）移动时，有必要将SFC迁移到合适的边缘服务器上。



服务的迁移，同样也是和移动用户相关，可以借鉴



## COPA: A Combined Autoscaling Method for Kubernetes

提出了一种称为 COPA 的新型组合缩放方法。 COPA根据收集到的微服务性能数据、实时工作负载、预期响应时间和运行时的微服务实例方案，使用排队网络模型计算出一个旨在最小化默认成本和资源成本的组合扩展方案。 



好奇K8S的内部算法实现、以及怎么做的实验



## Data & Computation-Intensive Service Re-Scheduling In Edge Networks

提出了一种能源感知数据和计算密集型服务迁移和调度机制 (DCMS)，以将某些服务从其托管设备重新安排到请求指定的地理区域内的服务。



同样也是，涉及到服务的迁移



## Game Theory-Based Task Offloading and Resource Allocation for Vehicular Networks in Edge-Cloud Computing

提出了一种基于博弈论和强化学习（RL）的任务卸载和资源分配方案，名为 TORA。 具体来说，博弈论被用来确定用于提高服务质量 (QoS) 的最佳任务卸载策略。

同时应用RL实现ES的动态资源分配。 最后，通过对比实验验证了所提出方法的鲁棒性能。



强化学习，和现在做的相近，好奇博弈论和如何保证鲁棒性



## QoE-aware Data Caching Optimization with Budget in Edge Computing

服务提供商可以考虑缓存附近位置的数据，以相对较低的延迟为其应用用户提供服务。 

考虑了 QoE-aware 边缘数据缓存的这个问题，旨在在缓存预算下优化用户的整体 QoE。 我们首先建立优化模型并证明该问题的 NP 完备性。 我们提出了一种启发式方法，并在理论上证明了其逼近率，以有效解决大规模场景的问题。



预先建立缓存，也是可以和移动用户联系起来

