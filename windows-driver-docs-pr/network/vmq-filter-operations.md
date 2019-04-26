---
title: VMQ 筛选器操作
description: VMQ 筛选器操作
ms.assetid: e8a977e8-2622-461b-9ca0-4834d33d76c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d2d302ebbb59a912a22fe9a1b446528ad6b1d0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327643"
---
# <a name="vmq-filter-operations"></a>VMQ 筛选器操作





多个接收筛选器，并可以在接收队列上设置。 此外，当前 VMQ 实现支持筛选器上的传入数据包并检查虚拟局域网 (VLAN) 标识符的可选筛选器的目标媒体访问控制 (MAC) 地址。

下图显示了 VLAN 标识符和 MAC 地址测试、 筛选器和队列之间的关系。

![说明 vlan 标识符和 mac 地址测试、 筛选器和队列之间的关系的关系图](images/vmqfilter.png)

在上图中，网络数据包包含目标地址 (DA) 和 VLAN 标识符字段。 网络适配器硬件实现基于微型端口驱动程序收到并在网络适配器硬件中设置的设置队列的筛选器。 接收队列上设置筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

在此图中，有两个筛选器;每个筛选器比较目标地址和到传入数据包中的字段为 VLAN 标识符。 如果 VLAN 和 DA 测试匹配，然后符合为该筛选器条件，并传入的数据包分配给该队列。 如果有多个筛选器对队列和任何筛选器的匹配项，网络适配器将数据包分配给该队列中。

 

 





