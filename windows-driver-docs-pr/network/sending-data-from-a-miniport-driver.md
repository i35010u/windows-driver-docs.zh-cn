---
title: 从微型端口驱动程序发送数据
description: 从微型端口驱动程序发送数据
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e58ecc34baa7cf7333a8e7c4e8c5a80ddbb9d4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381190"
---
# <a name="sending-data-from-a-miniport-driver"></a>从微型端口驱动程序发送数据





下图说明了微型端口驱动程序发送操作。

![说明微型端口驱动程序的关系图发送操作](images/miniportsend.png)

NDIS 调用微型端口驱动程序[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)函数将链接列表所述的网络数据传输[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

微型端口驱动程序调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数以返回 NET 的链接的列表\_缓冲区\_列表结构到基础驱动程序，并返回发送请求的最终状态。

 

 





