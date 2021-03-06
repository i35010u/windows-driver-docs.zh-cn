---
title: 在 CoNDIS 中发送和接收数据
description: 在 CoNDIS 中发送和接收数据
keywords:
- 虚拟连接 WDK CoNDIS，数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2786e11e43cff9ae73ef026f6748fc156e88c389
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248766"
---
# <a name="sending-and-receiving-data-in-condis"></a>在 CoNDIS 中发送和接收数据





传输数据涉及到通过已建立并激活的 VC 发送或接收数据包。

**注意** 在为 VC 调用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)后，协议驱动程序不得调用 [**NdisCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)将数据发送到 vc。

 

CoNDIS 发送和接收函数类似于无连接发送和接收功能。 CoNDIS 和无连接接口的主要区别在于 (VCs) 管理虚拟连接。 有关无连接发送和接收操作的详细信息，请参阅 [发送和接收操作](send-and-receive-operations.md)。

在单个函数调用中，CoNDIS 驱动程序可以在每个网络缓冲区列表结构上发送多个具有多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer)结构的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构 \_ \_ 。 此外，CoNDIS 驱动程序还可以针对每个网络缓冲区 \_ \_ \_ 列表结构上具有多个网络缓冲区结构的多个网络缓冲区列表结构指示已完成的发送操作 \_ \_ 。

在接收路径中，CoNDIS 微型端口驱动程序可以提供网络 \_ 缓冲区 \_ 列表结构的列表来指示接收。 \_ \_ 微型端口驱动程序提供的每个网络缓冲区列表包含一个网络 \_ 缓冲区结构。 由于不同的协议绑定可以处理每个网络 \_ 缓冲区 \_ 列表结构，因此 NDIS 可以独立地将每个网络 \_ 缓冲区 \_ 列表结构返回到微型端口驱动程序。

支持 NDIS 5。*x* 及更早版本的驱动程序，CoNDIS 在传统 [**NDIS \_ 数据包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构和基于网络缓冲区的结构之间提供了一个转换层 \_ 。 CoNDIS 在网络 \_ 缓冲区结构和 NDIS 数据包结构之间执行必要的转换 \_ 。 为了避免由于转换而导致性能下降，必须更新 CoNDIS 驱动程序以支持网络 \_ 缓冲区结构，并且应支持 \_ \_ 所有数据路径中的多个网络缓冲区列表结构。

本节包括下列主题：

[\_从 CoNDIS 驱动程序发送网络缓冲区结构](sending-net-buffer-structures-from-condis-drivers.md)

[\_在 CoNDIS 驱动程序中接收网络缓冲区结构](receiving-net-buffer-structures-in-condis-drivers.md)

 

