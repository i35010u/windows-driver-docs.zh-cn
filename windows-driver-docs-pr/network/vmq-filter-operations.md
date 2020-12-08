---
title: VMQ 筛选器操作
description: VMQ 筛选器操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84c96c7d2b85aa9eff9afe9b78209de309ba4612
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805137"
---
# <a name="vmq-filter-operations"></a>VMQ 筛选器操作





可在接收队列中设置多个接收筛选器和。 此外，当前 VMQ 实现支持对目标媒体访问控制的筛选器 (传入数据包的 MAC) 地址和用于检查虚拟局域网 (VLAN) 标识符的可选筛选器。

下图显示了 VLAN 标识符与 MAC 地址测试、筛选器和队列之间的关系。

![阐释 vlan 标识符与 mac 地址测试、筛选器和队列之间的关系的关系图](images/vmqfilter.png)

在上图中，网络数据包包含一个目标地址 (DA) 和 VLAN 标识符字段。 网络适配器硬件基于微型端口驱动程序在网络适配器硬件中接收并设置的设置，在队列上实现筛选器。 有关在接收队列上设置筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

在此图中，有两个筛选器：每个筛选器将目标地址和 VLAN 标识符与传入数据包中的字段进行比较。 如果 VLAN 和 DA 测试均匹配，则满足该筛选器的条件，并将传入数据包分配给该队列。 如果队列中有多个筛选器，然后为任何筛选器匹配，则网络适配器会将数据包分配给队列。

 

 





