# PPNA 修改内容

## abstract

我们将复杂AIoT应用使用有向无环图进行了建模，将AIoT应用中各AI服务的不同部署策略对性能与成本影响建模成了一个多目标优化问题CA3D，并采用启发式算法进行了求解；此外，我们在阿里云的实际数据集上对我们的方法有效性进行了验证。



We modeled complex AIoT applications using directed acyclic graphs, and investigated the relationship between the AIOT application performance and the energy cost in the MEC based service system by modeling it into a multi-objective optimization problem, namely CA$^3$D problem.  And we solved it efficiently with the help of heuristic algorithm. Besides, with the actual data set of Alibaba Cloud, we conducted comprehensive experiments to evaluate the results of our approach



In addition to AIoT applications, our method is also transferable to a certain extent for cost-effectiveness optimization of performance for applications based on sequential invocation of multiple services with dependencies among them.



##### 超体积指标（HV，Hypervolume）：算法获得的非支配解集与参照点围成的目标空间中区域的体积。HV值越大，说明算法的综合性能越好。

investigated the  modeled the impact of different deployment strategies of AI services in AIoT applications on performance and cost into a multi-objective optimization problem CA3D, and used heuristic algorithms to perform Solve; In addition, we verified the effectiveness of our method on the actual data set of Alibaba Cloud.



除了AIoT应用，对于基于多个服务依次调用，各服务之间存在依赖关系的应用，对于他们的性能成本效益优化，我们的方法也有一定的可迁移性。



## motivation



### 阿里云



### montage









## 实验部分

审稿意见所说的是这些？（其他的参数已经探讨过了）

以下参数实验均采用 MOEA\D 算法，其中种群规模为200，迭代次数为200代，变异概率 0.1 ，交叉概率0.8。其中迭代次数会影响算法的收敛性，如果过早结束迭代，可能导致结果未收敛到算法能够达到的最优状态，较高的交叉概率能够增加种群多样性，实现对最优结果的充分探索、较低的变异概率能够在维持已有结果不发生太大变化的情况下为种群带来一些新的基因，避免陷入局部最优？



为了简洁性和控制变量，我们对一下采用的包括MOEA/D在内的进化算法均采用相同的参数配置：即初始种群为 200，迭代次数为 200，变异概率为0.1，交叉概率为0.8。其中迭代次数会影响算法的收敛性，如果过早结束迭代，可能导致结果未收敛到算法能够达到的最优状态，较高的交叉概率能够增加种群多样性，实现对最优结果的充分探索、较低的变异概率能够在维持已有结果不发生太大变化的情况下为种群带来一些新的基因，避免陷入局部最优。



For the sake of simplicity and control variables, we adopt the same parameter configuration for the following evolutionary algorithms including MOEA/D, that is, the initial population is 200, the number of iterations is 200, the mutation probability is 0.1 and the crossover probability is 0.8. Meanwhile, the initial population is generated randomly within the decision space.

==是否需要补充相关实验说明==

 ==The number of iterations will affect the convergence of the algorithm. If the iteration is ended too early, the result may not converge to the optimal state that the algorithm can achieve. A higher crossover probability can increase the diversity of the population and realize the full exploration of the optimal result. The low mutation probability can bring some new genes to the population while maintaining the existing results without much change, and avoid falling into the local optimum.==





在如下伪代码中，我们可以清晰看出 MOEA/D 算法的主要复杂度来自于第22-32行中的for循环，即对每个个体更新它们的相邻解，其中，个体数量为 N，相邻解数量为 T，对每个目标函数，都需要执行同样的操作，在我们的算法里，目标函数是2个，即C和T，由此可得，在一次进化迭代里，算法的时间复杂度为 O(2NT)，总体时间复杂度为 O(MAX_ITER * 2NT)。









在 fig.6 添加

the GEN in the fig means the evolution generation of the population, namely, GEN=115 means the curve shows the result of the algorithm when the population evolution generation is 115





### 统计实验

对于多目标优化，广泛采用的衡量算法性能的指标之一是HV(hypervolume)，它表示由**解集中的个体**与**参考点**在目标空间中所围成的超立方体的体积。HyperVolume 可以同时评价解集的收敛性与分布性，HV值越大，说明算法的综合性能越好。

我们基于同样的数据、超参数配置，运行了200次我们的算法，最终得到的HV的分布柱状图

可以看到，其中80%的hv数据都在0.70以上，说明我们的算法收敛性不错，在多数时候都能得到一个较好的结果



### Montage

为了说明我们方法的良好的可迁移性，我们使用 Montage design 的 DAG 数据，在不同规模的服务数上测试了我们的算法，其结果如下，服务数按 montage-1到montage-3 依次增大



0.7580116987228394

## Conclusion

context-aware AIoT Application Deployment



除此之外，对于CA3D问题的这套建模、求解方法可以轻易地迁移到任何各组件依次调用，具有偏序依赖关系、可以被视为有向无环图的应用中，对如何优化这类应用中各组件的部署以及资源的分配、从而达到性能和成本的最优平衡具有借鉴指导意义。

In addition, this set of modeling and solving methods for CA$^3$D problems can be easily transferred to any application in which the components have partial order dependence and can be regarded as directed acyclic graph. It has a reference and guidance significance on how to optimize the deployment of components and resource allocation in such applications so as to achieve the optimal balance between performance and cost.

## 对实验的说明

