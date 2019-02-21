---
title: 数据包合并接收筛选器
description: 数据包合并接收筛选器
ms.assetid: B5C17A9D-A495-4A3D-B53E-B10F53C732D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e8d8aa3f72516fe5234a77a52b5e42a927ffd60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547543"
---
#  <a name="packet-coalescing-receive-filters"></a>数据包合并接收筛选器


从 NDIS 6.30 [NDIS 接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh205393)已扩展为支持数据包合并。 有关数据包合并每个接收筛选器定义以下各项：

-   一组的各种协议标头，例如媒体访问控制 (MAC) 标头或目标端口的用户数据报协议 (UDP) 标头的目标地址的数据包中的字段。

-   与合并接收筛选器匹配的数据包合并由网络适配器的最长时间。 适配器使用此值设置在适配器上一个硬件计时器过期值。 只要计时器过期，适配器必须中断主机以便微型端口驱动程序可处理合并的数据包。

    **请注意**  在合并与接收筛选器匹配的第一个数据包并启动计时器，网络适配器必须合并其他数据包接收筛选器相匹配而无需重置并重新启动计时器。

     

过量驱动程序，例如协议和筛选器驱动程序，下载数据包合并通过发出的对象标识符 (OID) 集请求中接收到微型端口驱动程序筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 有关详细信息，请参阅[设置数据包合并接收筛选器](setting-packet-coalescing-receive-filters.md)。

过量驱动程序还可以查询数据包合并接收下载到微型端口驱动程序的筛选器。 基础驱动程序执行此操作通过发出的 OID 方法请求[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)微型端口驱动程序。 有关详细信息，请参阅[查询数据包合并接收筛选器](querying-packet-coalescing-receive-filters.md)。

 

 





