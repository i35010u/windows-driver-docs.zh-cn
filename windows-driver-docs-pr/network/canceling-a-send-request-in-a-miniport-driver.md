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
ms.openlocfilehash: 307089bbdd245845e670423ab4ec0b0bc2ddf760
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382800"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>在微型端口驱动程序中取消发送请求





下图说明了微型端口驱动程序取消发送操作。

![说明的微型端口驱动程序取消发送操作的关系图](images/miniportcancelsend.png)

协议、 筛选和中间驱动程序可以调用[ **NdisCancelSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscancelsendnetbufferlists)取消未完成发送请求。 这些基础驱动程序必须在发送请求之前将取消 id 的发送数据。

NDIS 调用微型端口驱动程序[ *MiniportCancelSend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_send)函数取消所有传输[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)用指定的取消标识符标记的结构。

微型端口驱动程序*MiniportCancelSend*函数执行以下操作：

1.  遍历的未完成发送请求指定的适配器并调用其列表[ **NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)获取的每个网络取消标识符\_缓冲区\_列表结构。 微型端口驱动程序进行比较的取消操作 ID 的 NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID 返回 NDIS 传递给取消 ID *MiniportCancelSend*。

2.  删除从所有 NET\_缓冲区\_列表结构取消标识符匹配的未完成其列表中的指定的取消标识符将请求发送。

3.  调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数的所有已取消 NET\_缓冲区\_列表结构，以返回结构。微型端口驱动程序设置状态字段中的 NET\_缓冲区\_列表结构到 NDIS\_状态\_发送\_已中止。

 

 





