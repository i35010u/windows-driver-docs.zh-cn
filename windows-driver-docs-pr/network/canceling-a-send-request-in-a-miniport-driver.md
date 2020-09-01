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
ms.openlocfilehash: 7e483ec7347cd8e30c5593c527823c2847e36b94
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210213"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>在微型端口驱动程序中取消发送请求





下图说明了微型端口驱动程序取消发送操作。

![说明微型端口驱动程序的图示取消发送操作](images/miniportcancelsend.png)

协议、筛选器和中间驱动程序可以调用 [**NdisCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists) 来取消未完成的发送请求。 在发出发送请求之前，这些过量驱动程序必须使用取消 ID 标记发送数据。

NDIS 调用微型端口驱动程序的 [*MiniportCancelSend*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send) 函数来取消使用指定的取消标识符标记的所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的传输。

微型端口驱动程序的 *MiniportCancelSend* 函数执行以下操作：

1.  遍历指定适配器的未处理发送请求列表，并调用 [**NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_get_net_buffer_list_cancel_id) ，以获取每个网络 \_ 缓冲区列表结构的取消标识符 \_ 。 微型端口驱动程序将 NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 id 返回的取消 Id \_ 与 NDIS 传递给 *MiniportCancelSend*的取消 id 进行比较。

2.  从所有网络 \_ 缓冲区列表结构中删除， \_ 其取消标识符与它的未处理发送请求列表中的指定取消标识符相匹配。

3.  为所有[**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)已取消的网络 \_ 缓冲区列表结构调用 NdisMSendNetBufferListsComplete 函数 \_ 以返回结构。微型端口驱动程序将网络缓冲区列表结构的 "状态" 字段设置 \_ \_ 为 "NDIS \_ 状态发送已中止" \_ \_ 。

 

