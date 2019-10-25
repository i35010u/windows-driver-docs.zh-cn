---
title: 从微型端口驱动程序发送数据
description: 从微型端口驱动程序发送数据
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e260119776a168aa13680a325a5d4d69eb3106
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841976"
---
# <a name="sending-data-from-a-miniport-driver"></a>从微型端口驱动程序发送数据





下图说明了微型端口驱动程序发送操作。

![说明微型端口驱动程序发送操作的示意图](images/miniportsend.png)

NDIS 调用微型端口驱动程序的[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数来传输由网络[ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的链接列表描述的网络数据。

微型端口驱动程序调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数，以将网络\_缓冲区\_列表结构的链接列表返回到过量的驱动程序，并返回发送请求的最终状态。

 

 





