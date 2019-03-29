---
title: 将接收筛选器移到虚拟端口
description: 将接收筛选器移到虚拟端口
ms.assetid: 6315FB18-3F57-43C2-B864-3759058092BB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79fa01624e4c06e40bc051106e1ea3382894634b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575460"
---
# <a name="moving-a-receive-filter-to-a-virtual-port"></a>将接收筛选器移到虚拟端口


设置对象标识符 (OID) 的基础驱动程序问题的请求[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)将接收筛选器从虚拟端口 (VPort) 移动到另一个VPort NIC 交换机上。 通常情况下，基础驱动程序，如虚拟化堆栈中，发出此 OID 请求，如果任意下列条件为 true:

-   虚拟化堆栈设置默认 VPort 接收筛选器。 此筛选器包含的媒体访问控制 (MAC) 地址和公开 HYPER-V 子分区中的虚拟机 (VM) 网络适配器的虚拟 LAN (VLAN) 参数。 这允许通过基于软件的综合数据路径访问的 VM 网络适配器和基础的网络适配器之间转发数据包。

    分配资源的 PCI Express (PCIe) 虚拟函数 (VF) 以及取景器附加到子分区后，虚拟化堆栈上 VF 创建非默认 VPort。 然后，虚拟化堆栈将默认 VPort 从 VM 网络适配器的接收筛选器移到 VPort 附加到 VF 非默认中。 这允许通过基于硬件的 VF 数据路径访问的 VM 网络适配器和基础的网络适配器之间转发数据包。

    有关这些数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

-   已从 HYPER-V 子分区中的来宾操作系统仍在运行分离 VF。 在这种情况下，基础驱动程序将发出 OID 集请求，将 VM 网络适配器的接收筛选器从非默认 VPort 移到 VPort 附加到 PF.默认值 在此情况下，数据包流量将恢复为综合数据路径。

若要将接收筛选器从一个 VPort 移到另一个 VPort，基础驱动程序发出的 OID 集请求[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_移动\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构。

过量的驱动程序问题之前[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)请求，它必须初始化[ **NDIS\_接收\_筛选器\_移动\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451651)结构如下所示：

-   驱动程序集**FilterId**成员的标识符的以前分配的标识符的接收筛选器。

    **请注意**  过量的驱动程序从较早的 OID 方法请求获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)或[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。

     

-   驱动程序集**SourceQueueId**成员添加到 NDIS\_默认\_接收\_队列\_id。

-   驱动程序集**SourceVPortId**成员添加到以前在其设置此筛选器 VPort 的标识符。

-   驱动程序集**DestQueueId**成员添加到 NDIS\_默认\_接收\_队列\_id。

-   驱动程序集**DestVPortId**成员添加到此筛选器是要移动 VPort 的标识符。

NDIS 验证的成员[ **NDIS\_接收\_筛选器\_移动\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451651)将转发 OID 之前将请求设置为 PF 微型端口驱动程序。

当 PF 微型端口驱动程序处理此 OID 集请求时，它必须在原子操作中移动接收筛选器。 该驱动程序必须能够将网络适配器配置为同时从接收队列和 VPort 删除筛选器并将其设置其他接收队列和 VPort。

 

 





