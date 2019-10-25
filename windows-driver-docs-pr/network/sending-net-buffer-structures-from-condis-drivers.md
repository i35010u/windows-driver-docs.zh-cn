---
title: 从 CoNDIS 驱动程序发送 NET_BUFFER 结构
description: 从 CoNDIS 驱动程序发送 NET_BUFFER 结构
ms.assetid: 63bca3f0-b598-4006-bfd0-6df32ab2cbe7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565b0d2191098af0b3ea667979c32ea65d60379d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841971"
---
# <a name="sending-net_buffer-structures-from-condis-drivers"></a>从 CoNDIS 驱动程序发送 NET\_缓冲区结构





下图说明了一个基本的 CoNDIS 发送操作，该操作涉及一个协议驱动程序、NDIS 和一个微型端口驱动程序。

![说明基本 condis 发送操作（涉及协议驱动程序、ndis 和微型端口驱动程序）的示意图](images/netbuffercosend.png)

如上图所示，协议驱动程序调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)函数以将[**网络\_缓冲区发送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)虚拟连接（VC）上的列表结构。 然后，NDIS 调用微型端口驱动程序的[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数，将 NET\_缓冲区\_列表结构转发到基础微型端口驱动程序。

所有基于网络\_缓冲区的发送操作都是异步的。 因此，微型端口驱动程序始终调用[**NdisMCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)函数，并在发送完数据后提供相应的状态代码。 小型端口驱动程序可以针对每个网络\_缓冲区完成发送操作，\_列表结构与其他 NET\_缓冲区\_列表结构无关。 每次微型小型驱动程序调用**NdisMCoSendNetBufferListsComplete**时，NDIS 都调用协议驱动程序的[**ProtocolCoSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_send_net_buffer_lists_complete)函数。

当 NDIS 调用了协议驱动程序的*ProtocolCoSendNetBufferListsComplete*函数时，协议驱动程序可立即回收[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和所有关联的结构和数据的所有权。

微型端口驱动程序或 NDIS 可以按任意顺序返回\_缓冲区\_列表结构。 但会保证协议驱动程序无法修改附加到每个 NET\_\_缓冲区的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的列表。

协议驱动程序将[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的**SourceHandle**成员设置为与**NdisCoSendNetBufferLists**的*NdisVcHandle*参数相同的值。 NDIS 使用**SourceHandle**成员将 NET\_缓冲区\_列表结构返回到发送 NET\_缓冲区\_列表结构的协议驱动程序。

中间驱动程序还将 NET\_BUFFER\_列表结构中的**SourceHandle**成员设置为*NdisVcHandle*值。 如果中间驱动程序转发发送请求，则驱动程序必须保存过量驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS 向中间驱动程序返回已转发的 NET\_缓冲区\_列表结构时，中间驱动程序必须还原它保存的**SourceHandle** 。

协议驱动程序可以通过使用与无连接驱动程序相同的机制来取消发送请求。 有关取消发送请求的详细信息，请参阅[取消发送操作](canceling-a-send-operation.md)。

 

 





