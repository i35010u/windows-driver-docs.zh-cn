---
title: Hyper-V 可扩展交换机接口
description: Hyper-V 可扩展交换机接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb04279d0cb1ecadbbd6f67aa4824200ec146619
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836777"
---
# <a name="hyper-v-extensible-switch-interface"></a>Hyper-V 可扩展交换机接口


**注意**  本页假设你熟悉 [Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md) 和 [混合转发](hybrid-forwarding.md)概述中的信息和关系图。

 

Hyper-v 可扩展交换机是在 Hyper-v 父分区的管理操作系统中运行的虚拟以太网交换机。 可扩展交换机的每个实例都在主机中的物理网络接口与为 Hyper-v 子分区配置的虚拟网络接口之间路由数据包。 这些虚拟网络接口包括 Hyper-v 外部、内部和专用网络接口。

从 Windows Server 2012 中的 NDIS 6.30 开始，可扩展交换机模块支持一个接口，该接口允许 (称为 *可扩展交换机扩展*) 在可扩展交换机驱动程序堆栈内绑定的 NDIS 筛选器驱动程序。 这样，扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这样，扩展还可以在虚拟网络接口中检查和注入各种 Hyper-v 分区使用的数据包。

可以使用交换机和端口策略来配置扩展，以应用于通过可扩展交换机数据路径路由的数据包。 这允许驱动程序允许或拒绝通过端口发送或接收数据包。

在可扩展交换机接口中，筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。

可扩展交换机接口支持以下类型的扩展：

<a href="" id="capturing-extension"></a>捕获扩展  
捕获和监视数据包流量的扩展。 此类型的扩展无法通过可扩展交换机修改数据包或数据包目标。 但是，捕获扩展可能会产生数据包流量，例如包含扩展发送到主机应用程序的流量统计信息的数据包。

有关详细信息，请参阅 [捕获扩展](capturing-extensions.md)。

<a href="" id="filtering-extension"></a>筛选扩展  
捕获和监视数据包流量的扩展。 此类型的扩展还可以根据自定义端口或交换机策略设置来检查和拒绝数据包传送。

有关详细信息，请参阅 [筛选扩展](filtering-extensions.md)。

<a href="" id="forwarding-extension"></a>转发扩展  
与筛选扩展具有相同功能的扩展。 这种类型的扩展可以确定数据包传递到的可扩展交换机目标端口，还可以将数据包流量注入到任何可扩展交换机端口。 此类型的扩展还会检查并拒绝基于标准端口策略设置的数据包传送。

有关详细信息，请参阅 [转发扩展](forwarding-extensions.md)。

**注意**  在 NDIS 6.40 (Windows Server 2012 R2) 及更高版本中，转发扩展必须支持 [混合转发](hybrid-forwarding.md)。

 

**注意**  如果未在可扩展交换机中安装和启用转发扩展，则交换机会确定数据包的目标端口，并根据标准端口设置筛选数据包。

 

有关可扩展交换机接口的详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

 

 





