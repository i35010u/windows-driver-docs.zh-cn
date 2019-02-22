---
title: HYPER-V 可扩展交换机接口
description: HYPER-V 可扩展交换机接口
ms.assetid: 268AEA25-39D6-4494-B778-49C0B209E62E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d45bfbbce606c4f85d6aa2b40aff03acb82ec6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542843"
---
# <a name="hyper-v-extensible-switch-interface"></a>HYPER-V 可扩展交换机接口


**请注意**  此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

 

HYPER-V 可扩展交换机是虚拟以太网交换机的 HYPER-V 父分区在管理操作系统中运行。 可扩展交换机的每个实例之间路由数据包中主机的物理网络接口并为 HYPER-V 子分区配置的虚拟网络接口。 这些虚拟网络接口包括 HYPER-V 外部、 内部和专用网络接口。

从 Windows Server 2012 中的 NDIS 6.30，可扩展交换机模块支持一个允许 NDIS 筛选器驱动程序接口 (称为*可扩展交换机扩展*) 要在可扩展交换机驱动程序堆栈中绑定。 这允许扩展监视、 修改和将数据包转发到可扩展的交换机端口。 这也允许扩展以检查并注入中各种 HYPER-V 分区都使用的虚拟网络接口的数据包。

可以使用交换机和端口的策略，以将应用到通过可扩展交换机数据路径路由的数据包配置扩展。 这将允许驱动程序允许或拒绝来自发送或接收通过端口的数据包。

在可扩展交换机接口中，筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

可扩展交换机接口支持以下类型的扩展：

<a href="" id="capturing-extension"></a>捕获扩展  
一个扩展，捕获并监视数据包流量。 此类型的扩展不能修改数据包或数据包可通过可扩展交换机的目标。 但是，捕获扩展可以源自数据包流量，例如包，其中包含扩展将发送到主机应用程序的流量统计数据。

有关详细信息，请参阅[捕获扩展](capturing-extensions.md)。

<a href="" id="filtering-extension"></a>筛选扩展  
一个扩展，捕获并监视数据包流量。 此类扩展还可以检查和拒绝的数据包发送基于自定义端口或交换机策略设置。

有关详细信息，请参阅[筛选扩展](filtering-extensions.md)。

<a href="" id="forwarding-extension"></a>转发扩展  
扩展具有与筛选扩展相同的功能。 此类扩展可以确定的数据包发送到，可扩展交换机目标端口以及注入数据包流量发往任何可扩展交换机端口。 此类扩展还会检查并拒绝数据包发送基于标准端口策略设置。

有关详细信息，请参阅[转发扩展](forwarding-extensions.md)。

**请注意**  NDIS 6.40 (Windows Server 2012 R2) 中和更高版本、 转发扩展必须支持[混合转发](hybrid-forwarding.md)。

 

**请注意**  转发扩展未安装和启用了可扩展的交换机中，如果交换机确定数据包的目标端口以及筛选器基于标准的端口设置的数据包。

 

有关可扩展交换机接口的详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

 

 





