# ECS
ECS

ECS简介

Amazon Elastic Container Service (Amazon ECS) 是一种高度可扩展且快速的容器管理服务。 您可以使用它来运行、停止和管理集群上的容器。 使用 Amazon ECS，您的容器是在任务定义中定义的，您可以使用该任务定义来运行服务中的单个任务或任务。 在这种情况下，服务是一种配置，您可以使用它在集群中同时运行和维护指定数量的任务。 您可以在由 AWS Fargate 管理的无服务器基础设施上运行您的任务和服务。 或者，为了更好地控制您的基础设施，您可以在您管理的 Amazon EC2 实例集群上运行您的任务和服务。

部署方式说明

您可以使用两种模型来运行容器：
*Fargate 启动类型* - 这是一种无服务器即用即付选项。 您可以运行容器而无需管理您的基础设施。
*EC2 启动类型* - 在您的集群中配置和部署 EC2 实例以运行您的容器。
Fargate 启动类型适用于以下工作负载：

* 需要针对低开销进行优化的大型工作负载
* 偶尔爆发的小型工作负载
* 微小的工作量
* 批处理工作负载

EC2 启动类型适用于以下工作负载：

* 需要持续高 CPU 内核和内存使用率的工作负载
* 需要针对价格进行优化的大型工作负载
* 您的应用程序需要访问持久存储
* 您必须直接管理您的基础架构

其中，对于EC2部署方式，EC2的计费类别，有如下选项：

* 按需型实例（On Demand）：即可以按照实际需要随时启动，随时停止，但计费单价较高
* 竞价型示例（Spot）：AWS对于线上空置的资源，可以允许用户通过竞价方式以较低价格获取，但获取到的资源可能会被AWS随时回收

对于EC2的实例类型，也有如下选项：

* x86：x86芯片服务器
* arm：基于AWS自研的Graviton ARM芯片服务器，价格相较于x86较低，性价比更高

Fargate控制台部署示例

创建集群

* 选择创建集群

[Image: Image.jpg]
* 选择Networking Only

[Image: Image.jpg]
* 配置集群
    * 输入集群名称
    * 选择是否创建新的VPC
    * 如果要监控容器级别的指标，需勾选Enable Container Insight选项
    * 选择创建

[Image: Image.jpg]

定义任务

* 选择Create new Task Definition

[Image: Image.jpg]

* 选择Fargate

[Image: Image.jpg]

* Task definition name：填入自己的任务名称
* Task Role：选择默认的role
* Operating system family：选择linux
* Task execution role：选择默认
* Task memory (GB)：填入容器需要的内存
* Task CPU (vCPU)：填入容器需要的cpu
* Add container：添加容器描述

创建任务

* 回到Clusters界面
* 选择tasks
* 选择Run new tasks
* Launch Type：选择Fargate
* Operating system family：选择Linux
* Number of tasks：输入您需要并发运行的容器数量
* 选择下一步
* 选择集群VPC，子网和安全组
* Auto-assign public IP：选择enable



Spot控制台部署示例

创建集群

* 选择EC2 Linux+Networking

[Image: Image.jpg]


* Cluster name：填入集群名称
* Provisioning Model：选择spot
* Auto assign public IP：选择enable
* Spot Instance allocation strategy：选择Lowest price
* EC2 instance types：选择合适的实例类型，注意此处实例类型的cpu和内存，要大于容器所需资源
* CloudWatch Container Insights：选择Enable Container Insights

定义任务

* Launch type：选择EC2
* 基本如同上述定义任务

创建任务

* 基本如同上述创建任务

ECS性能监控

* 左上角服务搜索cloudwatch

[Image: Image.jpg]

* 选择Metrics- All metrics
* 在Browse里，即可发现对应的ECS的监控指标选项

[Image: Image.jpg]点击进入，可查看service级别的监控指标
[Image: Image.jpg]
