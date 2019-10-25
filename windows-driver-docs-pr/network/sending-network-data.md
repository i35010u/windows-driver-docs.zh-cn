---
title: 发送网络数据
description: 发送网络数据
ms.assetid: d3b960a7-bd2e-463c-b08b-5c3e4ecc36d0
keywords:
- 网络数据 WDK，发送
- 数据 WDK 网络，发送
- 包 WDK 网络，发送
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47398fa1404040303dd58fbcacd625ccfbbbe705
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841962"
---
# <a name="sending-network-data"></a>发送网络数据





下图说明了一个基本的发送操作，该操作涉及一个协议驱动程序、NDIS 和一个微型端口驱动程序。

![阐释基本 ndis 发送操作的关系图](images/netbuffersend.png)

协议驱动程序调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数以将[**网络\_缓冲区发送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)绑定上的列表结构。 NDIS 调用微型端口驱动程序的[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数，将 NET\_缓冲区\_列表结构转发到基础微型端口驱动程序。

所有基于网络\_缓冲区的发送操作都是异步的。 小型端口驱动程序在完成后使用适当的状态代码调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数。 每个 NET\_缓冲器\_列表结构的发送可以单独完成。 每次微型小型驱动程序调用**NdisMSendNetBufferListsComplete**时，NDIS 都调用协议驱动程序的[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数。

当 NDIS 调用协议驱动程序的*ProtocolSendNetBufferListsComplete*函数时，协议驱动程序可立即回收 NET\_缓冲区\_列表结构和所有关联的结构和数据的所有权。

微型端口驱动程序或 NDIS 可以按任意顺序返回[ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 协议驱动程序保证附加到每个 NET\_\_缓冲区的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)的列表尚未修改。

任何 NDIS 驱动程序都可以将 net\_缓冲区结构与网络\_缓冲区\_列表结构分离。 任何 NDIS 驱动程序还可以将\_网络中的 MDLs 分隔开来。 但是，驱动程序必须始终返回 NET\_缓冲区\_列表结构，其中包含 NET\_缓冲区结构和 MDLs 的原始形式。 例如，中间驱动程序可以将网络\_缓冲区\_列表分隔成两个新的 NET\_缓冲区\_列表结构，并将部分原始数据传递到下一个驱动程序。 但是，当中间驱动程序完成对原始 NET\_缓冲区的处理时\_列表，它必须返回完整的 NET\_缓冲区\_列表，其中包含原始 NET\_缓冲区结构和 MDLs。

协议驱动程序将 NET\_缓冲区\_列表结构中的**SourceHandle**成员设置为在对[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)函数的调用中提供的*NdisBindingHandle* 。 NDIS 使用**SourceHandle**成员将 NET\_缓冲区\_列表结构返回到发送 NET\_缓冲区\_列表结构的协议驱动程序。

中间驱动程序还将 NET\_BUFFER\_列表结构中的**SourceHandle**成员设置为在对**NdisOpenAdapterEx**的调用中提供的*NdisBindingHandle*值。 如果中间驱动程序转发发送请求，则驱动程序必须保存过量驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS 向中间驱动程序返回已转发的 NET\_缓冲区\_列表结构时，中间驱动程序必须还原它保存的**SourceHandle** 。

 

 





