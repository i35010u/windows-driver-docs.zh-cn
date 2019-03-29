---
title: 标头数据拆分体系结构
description: 标头数据拆分体系结构
ms.assetid: a2594360-cbac-4f77-840a-2572a2381646
keywords:
- 标头数据拆分 WDK，体系结构
- 标头数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3c4360f78c06d16486a52c7e8768ba31cd323d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565100"
---
# <a name="header-data-split-architecture"></a>标头数据拆分体系结构





标头数据拆分提供程序通过将标头和在接收到的以太网帧中的数据拆分为单独的缓冲区可以提高网络性能。 标头数据拆分提供程序包括网络接口卡 (NIC) 的 NDIS 6.1 或更高版本的微型端口驱动程序服务于 nic。

下图显示了标头数据拆分体系结构。

![说明标头数据的关系图分离的体系结构](images/hdsplitarchitecture.png)

微型端口驱动程序从 NDIS 设置 NIC 的标头数据拆分接收操作接收配置信息。 此外，微型端口驱动程序公开到 NDIS 的 NIC 的服务的运行时操作，如发送和接收操作。

NIC 的标头数据拆分操作能够接收以太网帧并拆分标头和数据到单独的接收缓冲区。

微型端口驱动程序使用正常的 NDIS 接收函数，以指示到 NDIS 接收到的数据。 此外，驱动程序必须分配一个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构时，该值指示接收到的数据。 有关详细信息，请参阅[，该值指示接收到的以太网帧](indicating-received-ethernet-frames.md)。

为标头数据拆分[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)中接收指示结构使用单独的内存描述符标头列表 (MDLs) 拆分接收的以太网帧和数据。 此外， [ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构包含标头数据拆分中 NET 信息\_缓冲区\_列表信息。

下图显示了接收的帧、 拆分缓冲区和标头缓冲区的内存布局。

![说明接收的帧、 拆分缓冲区和标头缓冲区的内存布局的关系图](images/hdspllitbuffers.png)

标头缓冲区都应在存储的连续块。

*上层协议*是如 TCP、 UDP 或 ICMP 的 IP 传输协议。

**请注意**  IPsec 时不考虑上层协议定义标头数据拆分要求的目的。 有关拆分 IPsec 帧的详细信息，请参阅[拆分 IPsec 帧](splitting-ipsec-frames.md)。

 

 

 





