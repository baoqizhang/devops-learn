### Namespace

Kubernetes in Action ：第3.7章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/namespaces/](https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/namespaces/)

学习视频：[https://www.youtube.com/watch?v=K3jNo4z5Jx8](https://www.youtube.com/watch?v=K3jNo4z5Jx8)

其他文档：[https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-namespace/](https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-namespace/)

### Label

Kubernetes in Action：第3.3、3.4、3.5章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/labels/](https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/labels/)

其他文档：[https://cast.ai/blog/kubernetes-labels-expert-guide-with-10-best-practices/](https://cast.ai/blog/kubernetes-labels-expert-guide-with-10-best-practices/)

### Pod

Kubernetes in Action：第3.1、3.2、3.6、3.8、4.1章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/workloads/pods/](https://kubernetes.io/zh-cn/docs/concepts/workloads/pods/)

学习视频：[P7](https://www.bilibili.com/video/BV1w4411y7Go?p=7&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)、[P18](https://www.bilibili.com/video/BV1w4411y7Go?p=18&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)、[https://www.youtube.com/watch?v=BgrQ16r84pM](https://www.youtube.com/watch?v=BgrQ16r84pM)

其他文档：[https://blog.aquasec.com/kubernetes-security-pod-escape-log-mounts](https://blog.aquasec.com/kubernetes-security-pod-escape-log-mounts)

### Replication Controller

Kubernetes in Action：第4.2 章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/replicationcontroller/](https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/replicationcontroller/)

视频：[P24](https://www.bilibili.com/video/BV1w4411y7Go?p=24&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)

### ReplicaSet

Kubernetes in Action：第4.3章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/replicaset/](https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/replicaset/)

视频：[P26](https://www.bilibili.com/video/BV1w4411y7Go?p=26&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)

### Deployment

Kubernetes in Action：第9章节

官方文档：[https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/deployment/](https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/deployment/)

视频：[P8](https://www.bilibili.com/video/BV1w4411y7Go?p=8&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)、[P27](https://www.bilibili.com/video/BV1w4411y7Go?p=27&vd_source=bf7e94c8b0d84f44941e85f9dac978a1)、[https://www.youtube.com/watch?v=iC-WxZGhFqs](https://www.youtube.com/watch?v=iC-WxZGhFqs)、[https://www.youtube.com/watch?v=7EZZXBbxRFs](https://www.youtube.com/watch?v=7EZZXBbxRFs)

其他文档：[https://www.baeldung.com/ops/kubernetes-deployment-vs-replicaset](https://www.baeldung.com/ops/kubernetes-deployment-vs-replicaset)、[https://www.bluematador.com/blog/kubernetes-deployments-rolling-update-configuration](https://www.bluematador.com/blog/kubernetes-deployments-rolling-update-configuration)

概览总结：[https://juejin.cn/post/6984954844293382181](https://juejin.cn/post/6984954844293382181)

### 达成目标：

- 完成Namespace、Label、Pod、Replication Controller、ReplicaSet、Deployment内容的学习(Kubernetes in Action对应章节的内容需要完成阅读、其他参考资料根据自身情况自行安排)

- 了解namespace的作用，并在minikube搭建的集群中创建dev\qa\uat\prod namespace

- 了解Label的作用

- 熟悉并掌握pod核心概念及作用

    - 编写Kubernetes Pod YAML文件(容器使用官方的Nginx镜像)且副本数为1

    - 为该Pod加上Lables（“app: nginx”和“env: {对应的环境}”）

    - 为该Pod加上存活探针

    - 在集群中运行该Pod至dev、prod namespace

    - 按照Pod名称删除

    - 使用标签选择器删除Pod

    - 通过删除整个命名空间来删除Pod

    - 删除命名空间所有的Pod，但保留命名空间

- 了解Replication Controller、ReplicaSet作用和区别

- 熟悉并掌握Deployment核心概念及作用

    - 改写Kubernetes Pod YAML文件为Kubernetes Deployment YAML文件，且副本数为2

    - 为该Deployment加上滚动升级策略

    - 为该Deployment加上就绪探针

    - 在集群中运行该Pod至dev namespace

    - 将Deployment中的Nginx容器升级至Nginx:1.21，并通过命令观察升级过程

    - 尝试调整滚动升级策略，再次将Nginx:1.21升级至Nginx:1.22，并通过命令观察升级过程

    - 尝试将Nginx:1.22回滚到Nginx:1.21，并观察回滚过程



