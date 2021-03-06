---
title: 从微型端口驱动程序发送数据
description: 从微型端口驱动程序发送数据
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c8ee1f33f8218300781b5a41888af424bbfb9ac
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247752"
---
# <a name="sending-data-from-a-miniport-driver"></a>从微型端口驱动程序发送数据





下图说明了微型端口驱动程序发送操作。

![说明微型端口驱动程序发送操作的示意图](images/miniportsend.png)

NDIS 调用微型端口驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数来传送网络 [**\_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的链接列表所描述的网络数据。

微型端口驱动程序调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数，以将网络缓冲区列表结构的链接列表返回 \_ \_ 到过量驱动程序，并返回发送请求的最终状态。

 

