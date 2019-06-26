---
title: 暂停适配器
description: 暂停适配器
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- 微型端口适配器 WDK 连接网络、 暂停
- 适配器 WDK 连接网络、 暂停
- 正在暂停状态 WDK 网络
- 暂停的状态 WDK 网络
- MiniportPause
- 正在暂停微型端口适配器
- 正在停止微型端口适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 539983513a04940149343b3867bdd8af6caa7ddc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382620"
---
# <a name="pausing-an-adapter"></a>暂停适配器





NDIS 调用微型端口驱动程序[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)函数以启动暂停操作。 暂停操作完成之前，适配器将仍处于暂停状态。

在暂停状态下，微型端口驱动程序必须完成未完成接收操作。 该驱动程序还必须完成任何未完成发送操作，它应拒绝任何新的发送请求。

若要完成接收操作，该驱动程序等待所有调用的[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数以返回 NDIS 必须返回所有未完成[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)微型端口驱动程序的结构[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

若要完成未完成发送操作，微型端口驱动程序应调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数的所有未完成的 NET\_缓冲区\_列表结构。 该驱动程序应拒绝对任何新的发送请求其[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)立即函数。

微型端口驱动程序完成所有未完成发送和接收操作后，该驱动程序必须同步或异步完成暂停请求。 如果以异步方式完成暂停操作，则该驱动程序调用[ **NdisMPauseComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismpausecomplete)完成暂停请求。 完成后暂停请求，微型端口驱动程序处于已暂停状态。

NDIS 并不会启动其他插操作、 暂停工作，如初始化、 电源更改，或重新启动操作，微型端口驱动程序处于暂停状态时。 NDIS 可以启动这些插操作后的微型端口驱动程序处于已暂停状态。

 

 





