---
title: NET_BUFFER 结构
description: NET_BUFFER 结构
keywords:
- NET_BUFFER
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
- NDIS_PACKET
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41c722cca42af7fa83446252e25838647c7b001
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810003"
---
# <a name="net_buffer-structure"></a>网络 \_ 缓冲区结构





NDIS 6.0 和更高版本的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构类似于 ndis 5 使用的 [**ndis \_ 数据包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构。*x* 及更早版本的驱动程序。 每个网络 \_ 缓冲区结构将网络数据数据包打包。

下图显示了网络缓冲区结构中的字段 \_ 。

![阐释网络缓冲区结构中的字段的关系图 \-](images/netbuffer.png)

NET \_ buffer 结构包含 **NetBufferHeader** 成员中的 [**网络 \_ 缓冲区 \_ 标头**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_header)结构。 NET \_ buffer \_ 标头结构包含 **NetBufferData** 成员中的 [**网络 \_ 缓冲区 \_ 数据**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)结构。 应使用 NDIS 宏来访问 NET \_ BUFFER 结构成员。 有关这些宏的完整列表，请参阅 [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) structure 参考页。

某些 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构成员仅由 NDIS 使用。 驱动程序通常使用的成员包括：

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
保留以供协议驱动程序使用。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
保留供微型端口驱动程序使用。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
指定一个池句柄，该句柄标识从中 \_ 分配网络缓冲区的网络缓冲池 \_ 。

<a href="" id="next"></a>**一个**  
指定一个指针，该指针指向 \_ 网络缓冲区结构的链接列表中的下一个网络缓冲区结构 \_ 。 如果这是列表中的最后一个网络 \_ 缓冲区结构，则此成员为 **NULL**。

<a href="" id="datalength"></a>**DataLength**  
指定 MDL 链中网络数据的长度（以字节为单位）。

<a href="" id="dataoffset"></a>**数据偏移量**  
指定从 MDL 链中的内存开始到 MDL 链中网络数据开始处的偏移量（以字节为单位）。

<a href="" id="currentmdl"></a>**CurrentMdl**  
指定指向当前驱动程序正在使用的第一个 MDL 的指针。 此指针提供优化，通过跳过当前驱动程序未使用的任何 MDLs 来提高性能。

<a href="" id="currentmdloffset"></a>**CurrentMdlOffset**  
指定由网络缓冲区结构的 **CurrentMdl** 成员指定的 MDL 中已用数据空间开始处的偏移量（以字节为单位） \_ 。

下图显示了 **CurrentMdl**、 **CurrentMdlOffset**、 **数据偏移量** 和 **DataLength** 成员与数据空间之间的关系。

![说明数据空间分配的关系图](images/netbufferdata-wmdl.png)

NDIS 提供了用于管理 MDL 链中的数据空间的函数。 驱动程序如何使用当前驱动程序与数据空间动态变化。 有时当前驱动程序当前未使用数据空间。 尽管未使用的 *数据空间* 当前未使用，但它可以包含有效数据。 例如，在接收路径上， *未使用的数据空间* 可以包含较低级别驱动程序使用的标头信息。

驱动程序执行撤回和高级操作，增加和减少已 *用的数据空间*。 有关撤回和高级操作的详细信息，请参阅 [撤回和高级操作](retreat-and-advance-operations.md)。

以下术语和定义描述了 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 数据空间的元素：

<a href="" id="used-data-space"></a>已用数据空间  
已 *用数据空间* 包含当前驱动程序当前正在使用的数据。 驱动程序使用撤回操作增加了 *使用的数据空间* ，并通过高级操作减少了 *使用的数据空间* 。

<a href="" id="unused-data-space"></a>未使用的数据空间  
当前驱动程序当前未使用此数据空间。

<a href="" id="total-data-size"></a>总数据大小  
"总数据大小" 是所 *用数据空间* 和 *未使用数据空间* 的大小之和。 若要计算总大小，请将 **数据偏移量** 添加到 **DataLength** 中。

<a href="" id="retreat"></a>撤回  
撤回操作会增加所 *用数据空间* 的大小。

<a href="" id="advance"></a>进  
高级操作将减小所 *用数据空间* 的大小。

 

