---
title: OID 请求的 Hyper-V 可扩展交换机控制路径
description: OID 请求的 Hyper-V 可扩展交换机控制路径
ms.assetid: 69ABBD54-F794-4A0A-8F50-915CA1EDD95C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82630bfc03c5292b7ec3369d52608c463635bd27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823920"
---
# <a name="hyper-v-extensible-switch-control-path-for-oid-requests"></a>OID 请求的 Hyper-V 可扩展交换机控制路径


本主题讨论 Hyper-v 可扩展交换机对象标识符（OID）请求在其上移动的控制路径。

下图显示了适用于 NDIS 6.40 的 OID 请求的可扩展交换机控制路径（Windows Server 2012 R2）和更高版本。

![用于 ndis 6.40 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath-ndis640.png)

下图显示了 NDIS 6.30 （Windows Server 2012）的 OID 请求的可扩展交换机控制路径。

![用于 ndis 6.30 的 vswitch oid 控制路径示意图](images/vswitch-oid-controlpath.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

可扩展交换机扩展（如筛选和转发扩展）负责根据端口或交换机策略允许或拒绝数据包流量。 为了使这些扩展应用策略决策，这些扩展必须能够执行以下操作：

-   从可扩展交换机接口接收有关可扩展交换机、其端口及其网络适配器连接的新的或更新的配置和状态的必要信息。

-   从可扩展交换机接口接收有关交换机或端口策略的新属性或更新属性的必要信息。

-   向可扩展交换机接口发出 OID 请求，以获取可扩展交换机、其端口及其网络适配器连接的当前配置。

可扩展交换机接口通过发出可扩展的交换机 OID 集请求，通知基础扩展对其组件配置和策略参数所做的更改。 这些请求由可扩展交换机的协议边缘颁发，通知基础扩展有关这些更改的信息。 这些 OID 请求在可扩展交换机驱动程序堆栈到可扩展交换机的基础微型端口边缘之间移动。

可扩展交换机的微型端口边缘负责完成 OID 请求。 但是，对于某些可扩展的开关 OID 请求，基础扩展可能会失败 OID 请求，从而拒绝通知。 例如，当可扩展交换机的协议边缘通知有关将创建的新端口的扩展时，它会发出 oid [\_switch\_端口\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)的 oid 设置请求。 基础筛选或转发扩展可以通过完成 OID 请求来拒绝端口创建，状态\_数据\_不\_接受。 有关此过程的详细信息，请参阅[接收 OID 有关 Hyper-v 可扩展交换机配置更改的请求](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)。

**请注意**  如果扩展不会拒绝可扩展的 switch OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

 

  **注意**使用[**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter)的堆栈重新启动请求将不会在可扩展的 switch OID 请求挂起时完成。 出于此原因，等待堆栈重新启动的扩展必须完成任何正在进行的 OID 请求。

 

大多数可扩展交换机 OID 请求只能由可扩展交换机接口发出。 但是，可以通过扩展颁发一些可扩展的交换机 OID 请求，以获取有关可扩展交换机、端口和网络适配器连接的配置的信息。 有关详细信息，请参阅[查询 Hyper-v 可扩展交换机配置](querying-the-hyper-v-extensible-switch-configuration.md)。

 

 





