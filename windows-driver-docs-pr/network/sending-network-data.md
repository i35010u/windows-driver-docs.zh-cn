---
title: 发送网络数据
description: 发送网络数据
ms.assetid: d3b960a7-bd2e-463c-b08b-5c3e4ecc36d0
keywords:
- 网络数据 WDK，发送
- 数据 WDK 连接网络、 发送
- 数据包 WDK 连接网络、 发送
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6853384772288d9c45592d8c518f61cf4feb5fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386842"
---
# <a name="sending-network-data"></a>发送网络数据





下图说明了一个基本的发送操作，这涉及到协议驱动程序、 NDIS 和微型端口驱动程序。

![说明基本 ndis 的关系图发送操作](images/netbuffersend.png)

协议驱动程序调用[ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)函数来发送[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)绑定上的结构。 NDIS 调用微型端口驱动程序[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)函数将转发 NET\_缓冲区\_列表结构为基础的微型端口驱动程序。

所有的 NET\_基于缓冲区的发送操作是异步的。 微型端口驱动程序调用[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数完成后，相应的状态代码。 发送的每个 NET\_缓冲区\_列表结构可以单独完成。 NDIS 调用协议驱动程序[ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数每个时间微型端口驱动程序调用**NdisMSendNetBufferListsComplete**。

协议驱动程序可以回收的 NET 所有权\_缓冲区\_列表结构和所有关联的结构和数据 NDIS 调用协议驱动程序时，就立即*ProtocolSendNetBufferListsComplete*函数。

可以返回的微型端口驱动程序或 NDIS [ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)按任意顺序的结构。 保证的协议驱动程序的列表[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构附加到每个网络\_缓冲区\_列表结构尚未修改。

任何 NDIS 驱动程序可以分隔 NET\_网络中的缓冲区结构\_缓冲区\_列表结构。 任何 NDIS 驱动程序，还可以将在 NET MDLs\_缓冲区结构。 但是，该驱动程序必须始终返回 NET\_缓冲区\_NET 具有列表结构\_缓冲区结构和 MDLs 以原始格式。 例如，中间驱动程序可能会单独 NET\_缓冲区\_列表到两个新的 NET\_缓冲区\_列表结构并将原始数据的一部分传递给下一步的驱动程序。 但是，当中间驱动程序完成处理的原始 NET\_缓冲区\_列表，它必须返回完整的 NET\_缓冲区\_列表中的以原始 NET\_缓冲区结构和MDLs。

协议驱动程序集**SourceHandle**中 NET 成员\_缓冲区\_列表结构*NdisBindingHandle*的调用中提供的 NDIS [ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)函数。 使用 NDIS **SourceHandle**要返回 NET 成员\_缓冲区\_给发送 NET 协议驱动程序的列表结构\_缓冲区\_列表结构。

中间驱动程序还设置**SourceHandle**成员在 NET\_缓冲区\_列表结构*NdisBindingHandle*值调用中提供该NDIS**NdisOpenAdapterEx**。 如果中间驱动程序将转发发送请求，该驱动程序必须将保存**SourceHandle**过量的驱动程序提供之前它将写入到的值**SourceHandle**成员。 当 NDIS 返回转发的 NET\_缓冲区\_必须还原到中间驱动程序，中间驱动程序的列表结构**SourceHandle**保存它。

 

 





