---
title: 在微型端口驱动程序中取消发送请求
description: 在微型端口驱动程序中取消发送请求
ms.assetid: 9339e661-b91a-49e1-9924-66c85cc80ee8
keywords:
- NdisCancelSendNetBufferLists
- MiniportCancelSend
- 取消发送请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6017c2daa559a47de37ca2a018ca8215dc049322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838214"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>在微型端口驱动程序中取消发送请求





下图说明了微型端口驱动程序取消发送操作。

![说明微型端口驱动程序的图示取消发送操作](images/miniportcancelsend.png)

协议、筛选器和中间驱动程序可以调用[**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)来取消未完成的发送请求。 在发出发送请求之前，这些过量驱动程序必须使用取消 ID 标记发送数据。

NDIS 调用微型端口驱动程序的[*MiniportCancelSend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)函数来取消使用指定的取消标识符标记的所有[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的传输。

微型端口驱动程序的*MiniportCancelSend*函数执行以下操作：

1.  遍历指定适配器的未处理发送请求列表并调用[**NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)以获取每个 NET\_缓冲区的取消标识符\_列表结构。 微型端口驱动程序会比较 NDIS\_获取\_NET\_缓冲区\_列表\_CANCEL\_ID 返回的取消 id，并将 NDIS 传递到*MiniportCancelSend*。

2.  从所有 NET\_缓冲区\_列表结构中删除，其取消标识符与它的未处理发送请求列表中指定的取消标识符相匹配。

3.  调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数，以使所有已取消的 NET\_缓冲区\_列表结构返回结构。微型端口驱动程序将 NET\_缓冲区\_列表结构的 "状态" 字段设置为 "NDIS\_状态"\_"已中止发送\_"。

 

 





