---
title: 在 CoNDIS 中发送和接收数据
description: 在 CoNDIS 中发送和接收数据
ms.assetid: aad7ccf9-0eaa-4327-b048-268d12593a70
keywords:
- 虚拟连接 WDK CoNDIS，数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339f0c8538eb2962e84ec502b338ec333eac6ac9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841979"
---
# <a name="sending-and-receiving-data-in-condis"></a>在 CoNDIS 中发送和接收数据





传输数据涉及到通过已建立并激活的 VC 发送或接收数据包。

**请注意**  协议驱动程序在为该 Vc 调用[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)后，不能调用[**NDISCOSENDNETBUFFERLISTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)将数据发送到 vc。

 

CoNDIS 发送和接收函数类似于无连接发送和接收功能。 CoNDIS 和无连接接口之间的主要区别是虚拟连接（VCs）的管理。 有关无连接发送和接收操作的详细信息，请参阅[发送和接收操作](send-and-receive-operations.md)。

在单个函数调用中，CoNDIS 驱动程序可以将多个 net [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构发送到每个网络\_缓冲区\_列表结构的多个 NET [ **\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 此外，CoNDIS 驱动程序还可以针对多个 net\_缓冲区\_列表结构的已完成发送操作\_，其中每个网络\_缓冲区\_列表结构。

在接收路径中，CoNDIS 微型端口驱动程序可以提供网络\_缓冲区的列表\_列表结构以指示接收。 每个网络\_缓冲区\_列表，微型端口驱动程序提供的包含一个网络\_缓冲区结构。 由于不同的协议绑定可以处理每个网络\_缓冲区\_列表结构，因此 NDIS 可以将每个 NET\_缓冲区单独返回到微型端口驱动程序的\_列表结构。

支持 NDIS 5。*x*及更早版本的驱动程序，CoNDIS 在旧版[**NDIS\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构和基于网络\_缓冲区的结构之间提供转换层。 CoNDIS 在 NET\_缓冲区结构与 NDIS\_数据包结构之间执行必要的转换。 为了避免由于转换而导致性能下降，必须更新 CoNDIS 驱动程序以支持 NET\_缓冲区结构，并且应支持所有数据路径中的多个 NET\_缓冲器\_列表结构。

本部分包括以下主题：

[从 CoNDIS 驱动程序发送 NET\_缓冲区结构](sending-net-buffer-structures-from-condis-drivers.md)

[在 CoNDIS 驱动程序中接收 NET\_缓冲区结构](receiving-net-buffer-structures-in-condis-drivers.md)

 

 





