---
title: 在 CoNDIS 中发送和接收数据
description: 在 CoNDIS 中发送和接收数据
ms.assetid: aad7ccf9-0eaa-4327-b048-268d12593a70
keywords:
- 虚拟连接 WDK 的 CoNDIS，数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24714e43ae8ba05bb37f5732bd347e03d8191202
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383642"
---
# <a name="sending-and-receiving-data-in-condis"></a>在 CoNDIS 中发送和接收数据





将数据传输涉及发送或通过已建立并激活 VC 接收数据包。

**请注意**  协议驱动程序不能调用[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)调用后将数据发送到 VC [ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)为该 VC。

 

CoNDIS 发送和接收函数类似于无连接发送和接收函数。 CoNDIS 和无连接的接口之间的主要区别是虚拟的连接 (VCs) 的管理。 详细了解无连接发送和接收操作，请参阅[发送和接收操作](send-and-receive-operations.md)。

在单个函数调用，CoNDIS 驱动程序可以发送多个[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构具有多个[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)每个网络上的结构\_缓冲区\_列表结构。 此外，驱动程序可以指示已完成的 CoNDIS 发送操作的多个 NET\_缓冲区\_具有多个网络的列表结构\_每个网络上的缓冲区结构\_缓冲区\_列表结构。

在接收路径的 CoNDIS 微型端口驱动程序可以提供一系列 NET\_缓冲区\_列表结构，以指示接收。 每个 NET\_缓冲区\_微型端口驱动程序提供的列表包含一个 NET\_缓冲区结构。 因为不同的协议绑定可以处理每个 NET\_缓冲区\_列表结构 NDIS 可以独立返回每个 NET\_缓冲区\_微型端口驱动程序的列表结构。

若要支持 NDIS 5。*x*和早期版本的驱动程序的 CoNDIS 提供旧版之间创建转换层[ **NDIS\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构和 NET\_缓冲区基于结构。 CoNDIS 执行必要的转换之间 NET\_缓冲区结构和 NDIS\_数据包结构。 若要避免由于转换会降低性能，必须将的 CoNDIS 驱动程序更新为支持 NET\_缓冲结构，并且应该支持多个 NET\_缓冲区\_中数据的所有路径的列表结构。

本部分包括以下主题：

[发送 NET\_缓冲区结构的 CoNDIS 驱动程序](sending-net-buffer-structures-from-condis-drivers.md)

[接收 NET\_缓冲区中的 CoNDIS 驱动程序的结构](receiving-net-buffer-structures-in-condis-drivers.md)

 

 





