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
ms.openlocfilehash: 40da73565e150e7dabc938f5f68b82b160e96d45
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208565"
---
# <a name="sending-network-data"></a>发送网络数据





下图说明了一个基本的发送操作，该操作涉及一个协议驱动程序、NDIS 和一个微型端口驱动程序。

![阐释基本 ndis 发送操作的关系图](images/netbuffersend.png)

协议驱动程序调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) 函数以发送绑定上的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 NDIS 调用微型端口驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数将网络 \_ 缓冲区 \_ 列表结构转发到基础微型端口驱动程序。

所有 \_ 基于网络缓冲区的发送操作都是异步的。 小型端口驱动程序在完成后使用适当的状态代码调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数。 每个网络 \_ 缓冲区 \_ 列表结构的发送可以单独完成。 每次微型小型驱动程序调用**NdisMSendNetBufferListsComplete**时，NDIS 都调用协议驱动程序的[**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数。

当 \_ \_ NDIS 调用了协议驱动程序的 *ProtocolSendNetBufferListsComplete* 函数时，协议驱动程序可以立即收回网络缓冲区列表结构和所有关联的结构和数据的所有权。

微型端口驱动程序或 NDIS 可以按任意顺序返回 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 协议驱动程序保证附加到每个网络缓冲区列表结构的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 的列表尚未 \_ \_ 修改。

任何 NDIS 驱动程序可以将网络 \_ 缓冲区结构与网络 \_ 缓冲区 \_ 列表结构分离。 任何 NDIS 驱动程序还可以将 MDLs 划分为网络 \_ 缓冲区的结构。 但是，驱动程序必须始终以 \_ 原始形式返回网络缓冲区 \_ 列表结构，其中包含 net \_ Buffer 结构和 MDLs。 例如，中间驱动程序可以将网络 \_ 缓冲区列表分隔 \_ 成两个新的网络 \_ 缓冲区 \_ 列表结构，并将部分原始数据传递到下一个驱动程序。 但是，当中间驱动程序完成对原始网络缓冲区列表的处理时， \_ \_ 它必须返回完整的网络 \_ 缓冲区 \_ 列表，其中包含原始的网络缓冲区 \_ 结构和 MDLs。

协议驱动程序将网络缓冲区列表结构中的**SourceHandle**成员设置 \_ \_ 为在对[**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)函数的调用中提供的*NdisBindingHandle* 。 NDIS 使用 **SourceHandle** 成员将网络 \_ 缓冲区 \_ 列表结构返回到发送网络 \_ 缓冲区列表结构的协议驱动程序 \_ 。

中间驱动程序还将 NET BUFFER LIST 结构中的**SourceHandle**成员设置 \_ \_ 为在对**NdisOpenAdapterEx**的调用中提供的*NdisBindingHandle*值。 如果中间驱动程序转发发送请求，则驱动程序必须保存过量驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS \_ \_ 向中间驱动程序返回已转发的网络缓冲区列表结构时，中间驱动程序必须还原它保存的 **SourceHandle** 。

 

