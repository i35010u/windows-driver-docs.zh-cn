---
title: 数据包合并接收筛选器
description: 数据包合并接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 849d0c5a4da85449cd2a3da515976211975aadf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797919"
---
#  <a name="packet-coalescing-receive-filters"></a>数据包合并接收筛选器


从 NDIS 6.30 开始， [ndis 接收筛选器](/windows-hardware/drivers/ddi/_netvista/) 已扩展为支持数据包合并。 数据包合并的每个接收筛选器都定义以下内容：

-   数据包的各个协议标头中的一组字段，例如媒体访问控制的目标地址 (MAC) 标头或用户数据报协议的目标端口 (UDP) 标头。

-   网络适配器合并与合并接收筛选器匹配的数据包的最长时间。 适配器使用此值在适配器上的硬件计时器上设置过期值。 计时器过期后，适配器必须中断主机，使微型端口驱动程序能够处理合并的数据包。

    **注意**  当首个匹配接收筛选器的数据包合并并启动计时器后，网络适配器必须合并与接收筛选器匹配的其他数据包，而无需重置和重新启动计时器。

     

使用过量驱动程序（如协议和筛选器驱动程序），可以通过 (OID 发出对象标识符) 设置 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的请求，将数据包合并接收筛选器下载到微型端口驱动程序。 有关详细信息，请参阅 [设置数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

过量驱动程序还可以查询下载到微型端口驱动程序的数据包合并接收筛选器。 过量驱动程序通过向微型端口驱动程序发出 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 的 oid 方法请求来实现此目的。 有关详细信息，请参阅 [查询数据包合并接收筛选器](querying-packet-coalescing-receive-filters.md)。

 

