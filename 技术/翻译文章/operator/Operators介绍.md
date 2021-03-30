# Operators
## 起因
在 Kubernetes 可以使用默认的控制器(DC、DS等)相对容易的管理和扩展无状态的应用(Web、移动后端、API等)。但管理有状态的应用程序，像数据库，缓存和监控系统则是更大的挑战。这些系统需要应用领域的知识才能正确扩展，升级和重新配置，从而防止数据丢失或不可用。我们希望将这种应用特定的操作知识编写到软件中，其可以使用利用强大的 Kubernetes 抽象能力，达到正确运行和管理应用程序的目的。

现场可靠性工程师（Site Reliability Engineer）是通过编写软件来管理应用程序的人员。 他们是工程师，开发人员，知道如何专门为特定的应用领域开发软件。由此产生将应用程序的运行的领域知识编入对应的软件（简单的说就是，产生了一个专门针对软件运行管理的软件领域，即 Operator）。

## 什么是 operator
Operator 是一种软件，它结合了特定的领域知识并通过 [third party resources](http://kubernetes.io/docs/user-guide/thirdpartyresources/) （CRD）机制扩展了Kubernetes API，使用户像管理 Kubernetes 的内置资源一样创建，配置和管理应用程序。Operator 管理整个集群中的多个实例，而不仅仅管理应用程序的单个实例。

![](./pic/Overview-etcd_0.png)

为了用实际运行代码演示 Operator 概念，今天我们宣布两个具体的开源项目：

1. [etcd Operator](https://coreos.com/blog/introducing-the-etcd-operator.html) 创建，配置和管理 etcd 群集。 
- [Prometheus Operator](https://coreos.com/blog/the-prometheus-operator.html) 创建，配置和管理 Prometheus 监控实例。 

## Operator 原理
Operators 建立在 Kubernetes 两个核心概念上：Resources 和 Controllers。 例如内置的 [ReplicaSet](http://kubernetes.io/docs/user-guide/replicasets/) 资源允许用户设置运行所需 Pod 的数量，并且 Kubernetes 内的 Controllers 通过创建或删除正在运行的 Pod 来确保在 ReplicaSet 资源中设置符合预期的状态。 Kubernetes 中有许多以这种方式工作的基础 controllers 和 resources，包括 [Services](http://kubernetes.io/docs/user-guide/services/), [Deployments](http://kubernetes.io/docs/user-guide/deployments/), 和 [Daemon Sets](http://kubernetes.io/docs/admin/daemons/) 等。

- 例 1
	- 运行的单个 Pod，用户修改期望运行的 Pod 数目为 3

		![](./pic/RS-before.png)

	- 一段时间后，Kubernetes 内部的 controllers 创建了更多的 Pod 以满足用户要求

		![](./pic/RS-scaled.png)

Operator 建立在基本的 Kubernetes resource 和 controller 概念之上，增加了一套知识或配置，允许 Operator 执行常见的应用任务。 
	
例如手动扩展一个 etcd 集群时，用户必须执行多个步骤：
	
- 为新的 etcd 成员创建一个 DNS 名称
- 启动新的 etcd 实例
- 然后使用 etcd 管理工具（etcdctl member add）告诉关于这个新成员的现有集群。 
- 等
	
而使用 etcd Operator 用户可以简单通过 etcd 集群大小增加 1。

![](./pic/Operator-scale.png)

- 例 2: 用户使用 kubectl 触发了备份操作

	Operator 可能处理的复杂管理任务的其他示例包括安全协调应用程序升级，配置备份到异地存储，通过本地 Kubernetes API 进行服务发现，应用程序 TLS 证书配置和灾难恢复。

## 如何创建 Operator？
Operators 本质上是特定于应用程序，所以最复杂的工作是将应用程序运转的领域知识编码为合理的配置资源和控制循环。在构建任何应用程序都很重要的 Operators 时，发现了一些常见模式：

1. Operators 应该像部署单个 deployment 一样进行部署，并在安装后不需要再执行其他操作。

	例如 `kubectl create -f https://coreos.com/operators/etcd/latest/deployment.yaml` 
- Operators 在部署到 Kubernetes 时应创建一个新的第三方类型。用户使用此类型创建新的应用程序实例。
- Operators 应尽可能利用内置的 Kubernetes 原语，如 Services 和 Replica Sets，以充分利用经过良好测试和易于理解的代码。
- Operators 应该向后兼容并且始终了解用户创建的以前版本的资源。
- Operators 应被设计成 Operators 停止或删除时应用程序实例不受影响。
- Operators 应该让用户能够根据声明的期望版本进行对应的编排应用程序升级。不进行软件升级是操作错误和安全问题的根源
- Operators 可以帮助用户更加方便地解决这一问题。
- Operators 应该针对潜在的Pod，配置和网络故障的使用 “Chaos Monkey” 测试套件进行测试。

## Operators 的前景分析



## FAQ
- 问：这与StatefulSets（以前的PetSets）有什么不同？

	答：StatefulSets 旨在支持 Kubernetes 中的应用程序，这些应用程序需要群集为静态IP和存储提供 “有状态资源”。 需要这种更有状态的部署模型的应用程序仍然需要 Operator 自动化来提醒并针对故障，备份或重新配置采取行动。 因此需要这些部署属性的应用程序的 Operators 可以使用 StatefulSets，而不是利用 ReplicaSets 或Deployments。

- 问：这与 Puppet 或 Chef 等配置管理有何不同？

	答：Containers 和 Kubernetes 是使 Operators 成为与他们有了巨大差异。 结合这两种技术，使用 Kubernetes API，部署新软件，协调分布式配置以及检查多主机系统状态是一致且容易的。Operators 这些原语粘贴在一起，为应用程序使用者提供有用的方式； 它不仅仅是配置，而是整个应用状态。

- 问：这与 Helm 有什么不同？

	答：Helm是一个将多个 Kubernetes 资源打包到一个包中的工具。 将多个应用程序打包在一起并使用主动管理应用程序的操作员是相辅相成的概念。 例如，traefik 是一个可以使用 etcd 作为其后端数据库的负载平衡器。 您可以创建一个Helm Chart，将 traefik Deployment 和 etcd 集群实例一起部署。 etcd 集群将由 etcd Operator部署和管理。

- 问：如果是 Kubernetes新手？ 这是什么意思？

	答：这不应该改变新用户的任何内容，除非让他们更容易在将来部署诸如 etcd，Prometheus 等的复杂应用程序。 我们推荐的 Kubernetes 入门路径仍然是 minikube，kubectl run，然后可能会开始与 Prometheus Operator 一起玩，以监控您使用 kubectl run 部署的应用程序。

- 问: Operator 和 Prometheus 代码今天是否可用?

	A: 是的，你可以在 GitHub https://github.com/coreos/etcd-operator 和 https://github.com/coreos/prometheus-operator 找到他们


问：有其他 Operators 的计划吗？

答：是的，这很可能在未来。 我们也很乐意看到新的 Operators 也得到了社区的建立。 让我们知道您希望看到的其他运营商下一步要做什么。

备注：mysql operator

问：Operators 如何帮助确保群集安全？

答：不升级软件是操作错误和安全问题的常见来源，Operators 可以帮助用户更加自信地解决执行正确升级的难题。

问：Operators 可以帮助灾难恢复吗？

答：Operators 可以轻松定期备份应用程序状态并从备份中恢复以前的状态。 我们希望 Operators 能够普遍使用这一项功能可以让用户轻松地从备份中部署新实例。

## 原文链接
- https://coreos.com/blog/introducing-operators.html
- https://www.do1618.com/archives/1255/operators-%E4%BB%8B%E7%BB%8D/
- https://sdk.operatorframework.io/#