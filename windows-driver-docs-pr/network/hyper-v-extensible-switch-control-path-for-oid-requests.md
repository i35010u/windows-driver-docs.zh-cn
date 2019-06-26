---
title: OID 请求的 Hyper-V 可扩展交换机控制路径
description: OID 请求的 Hyper-V 可扩展交换机控制路径
ms.assetid: 69ABBD54-F794-4A0A-8F50-915CA1EDD95C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c17da023d8e4373fe6b21dbc55c60c649e8e0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383720"
---
# <a name="hyper-v-extensible-switch-control-path-for-oid-requests"></a>OID 请求的 Hyper-V 可扩展交换机控制路径


本主题讨论在之间移动的 HYPER-V 可扩展交换机对象标识符 (OID) 请求的控制路径。

下图显示了 OID 请求 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机控制路径。

![ndis 6.40 的 vswitch oid 控制路径的关系图](images/vswitch-oid-controlpath-ndis640.png)

下图显示 OID 请求的可扩展交换机控制的路径的 NDIS 6.30 (Windows Server 2012)。

![ndis 6.30 的 vswitch oid 控制路径的关系图](images/vswitch-oid-controlpath.png)

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*.

 

可扩展交换机扩展，如筛选和转发扩展，负责允许或拒绝数据包流量根据端口或交换机的策略。 为了使这些扩展来应用策略决策，这些扩展必须能够执行以下操作：

-   获得有关新的或更新的配置和状态的可扩展交换机、 其端口和其网络适配器连接的可扩展交换机接口所需的信息。

-   有关交换机或端口的策略的新的或更新属性的可扩展交换机接口获得所需的信息。

-   若要获取可扩展交换机、 其端口和其网络适配器连接的当前配置的可扩展交换机接口向发出 OID 请求。

可扩展交换机接口通知有关的组件配置更改的基础扩展，并通过发出可扩展的策略参数切换 OID 集请求。 这些请求颁发的可扩展的交换机，以通知有关这些更改的基础扩展的协议边缘。 这些 OID 请求将通过可扩展交换机驱动程序堆栈移到可扩展交换机的基础的微型端口边缘。

可扩展交换机的微型端口边缘负责完成 OID 请求。 但是，某些可扩展交换机 OID 请求，与基础扩展可能失败 OID 请求，以便能阻止通知。 例如，当可扩展交换机的协议边缘通知时将创建新端口有关的扩展，它发出的 OID 集请求[OID\_切换\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)。 基础筛选或转发扩展可通过完成状态为 OID 请求否决端口创建\_数据\_不\_已接受。 此过程的详细信息，请参阅[有关的 HYPER-V 可扩展交换机配置更改接收 OID 请求](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)。

**请注意**  如果扩展不能阻止可扩展交换机 OID 请求，请求完成时，它应监视状态。 该扩展应这样做可以确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

 

**请注意**  堆栈重新启动使用请求[ **NdisFRestartFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfrestartfilter)可扩展交换机 OID 请求挂起时，将不会完成。 出于此原因，正在等待堆栈重新启动的扩展必须完成任何正在进行的 OID 请求。

 

只可由可扩展交换机接口发出大多数可扩展交换机 OID 请求。 但是，某些可扩展交换机 OID 请求可以发出由扩展以获取有关配置的可扩展交换机、 其端口和其网络适配器连接的信息。 有关详细信息，请参阅[查询的 HYPER-V 可扩展交换机配置](querying-the-hyper-v-extensible-switch-configuration.md)。

 

 





