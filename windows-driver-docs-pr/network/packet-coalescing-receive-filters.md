---
title: 数据包合并接收筛选器
description: 数据包合并接收筛选器
ms.assetid: B5C17A9D-A495-4A3D-B53E-B10F53C732D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 202b0cb15a76efe286058b3106b3c76ae2c36cda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843720"
---
#  <a name="packet-coalescing-receive-filters"></a>数据包合并接收筛选器


从 NDIS 6.30 开始， [ndis 接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)已扩展为支持数据包合并。 数据包合并的每个接收筛选器都定义以下内容：

-   数据包的各个协议标头中的一组字段，例如用户数据报协议（UDP）标头的媒体访问控制（MAC）标头或目标端口的目标地址。

-   网络适配器合并与合并接收筛选器匹配的数据包的最长时间。 适配器使用此值在适配器上的硬件计时器上设置过期值。 计时器过期后，适配器必须中断主机，使微型端口驱动程序能够处理合并的数据包。

    **请注意**  只要匹配接收筛选器的第一个数据包合并并启动计时器，网络适配器必须合并与接收筛选器匹配的其他数据包，而无需重置和重新启动计时器。

     

使用过量驱动程序（如协议和筛选器驱动程序），可以通过发出[OID\_接收\_filter\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)发出对象标识符（oid）设置请求，将数据包合并接收筛选器下载到微型端口驱动程序。 有关详细信息，请参阅[设置数据包合并接收筛选器](setting-packet-coalescing-receive-filters.md)。

过量驱动程序还可以查询下载到微型端口驱动程序的数据包合并接收筛选器。 过量驱动程序通过发出 Oid 的 OID 方法请求来实现此目的[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)发送到微型端口驱动程序。 有关详细信息，请参阅[查询数据包合并接收筛选器](querying-packet-coalescing-receive-filters.md)。

 

 





