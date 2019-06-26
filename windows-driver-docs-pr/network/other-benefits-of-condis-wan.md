---
title: CoNDIS WAN 的其他优势
description: CoNDIS WAN 的其他优势
ms.assetid: 5b937ae4-1486-4563-a863-5c02ba57c7df
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络权益
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01cf14061446710d91a9e80c5360464f2ed378bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366533"
---
# <a name="other-benefits-of-condis-wan"></a>CoNDIS WAN 的其他优势





灵活、 更简单，除了 CoNDIS WAN 模型还提供以下优势：

-   WAN 的 CoNDIS 微型端口驱动程序支持 multipacket[发送和接收操作](sending-and-receiving-data.md)。

-   当 CoNDIS 微型端口驱动程序指示接收数据包时，绑定的协议可以延迟处理的数据包。 在 NDIS WAN 的微型端口驱动程序指示接收数据包，绑定的协议必须立即将数据复制。

-   WAN 的 CoNDIS 支持多点调用。 有关进行多点调用的详细信息，请参阅[进行调用](making-a-call.md)。

-   WAN 的 CoNDIS 支持服务的质量 (QoS)。 WAN 的 CoNDIS 驱动程序使用[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 有关的 CoNDIS QoS 的详细信息，请参阅[Client-Initiated 请求更改调用参数](client-initiated-request-to-change-call-parameters.md)。

-   只有 CoNDIS WAN 将支持未来的 NDIS 增强功能适用于 WAN 的驱动程序。

 

 





