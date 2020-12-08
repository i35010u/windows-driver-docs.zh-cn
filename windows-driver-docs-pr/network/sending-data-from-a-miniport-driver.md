---
title: 从微型端口驱动程序发送数据
description: 从微型端口驱动程序发送数据
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e659fe8f5d122b8ff1dd12f330b3b2df6626f2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840277"
---
# <a name="sending-data-from-a-miniport-driver"></a>从微型端口驱动程序发送数据





下图说明了微型端口驱动程序发送操作。

![说明微型端口驱动程序发送操作的示意图](images/miniportsend.png)

NDIS 调用微型端口驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数来传送网络 [**\_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表所描述的网络数据。

微型端口驱动程序调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数，以将网络缓冲区列表结构的链接列表返回 \_ \_ 到过量驱动程序，并返回发送请求的最终状态。

 

