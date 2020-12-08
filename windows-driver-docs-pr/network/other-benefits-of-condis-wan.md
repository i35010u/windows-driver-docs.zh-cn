---
title: CoNDIS WAN 的其他优势
description: CoNDIS WAN 的其他优势
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbc32ee1a31e0687e8aeaefa220198240b9aa50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793423"
---
# <a name="other-benefits-of-condis-wan"></a>CoNDIS WAN 的其他优势





除了灵活性和简洁性外，CoNDIS WAN 模型还提供以下优势：

-   CoNDIS WAN 微型端口驱动程序支持 multipacket [发送和接收操作](sending-and-receiving-data.md)。

-   当 CoNDIS 微型端口驱动程序指示接收数据包时，绑定协议可能会延迟数据包的处理。 当 NDIS WAN 微型端口驱动程序指示接收数据包时，绑定协议必须立即复制数据。

-   CoNDIS WAN 支持 multipoint 调用。 有关进行 multipoint 调用的详细信息，请参阅 [进行呼叫](making-a-call.md)。

-   CoNDIS WAN 支持 (QoS) 的服务质量。 CoNDIS WAN 驱动程序使用 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 有关 CoNDIS QoS 的详细信息，请参阅 [客户端启动的更改调用参数的请求](client-initiated-request-to-change-call-parameters.md)。

-   只有 CoNDIS WAN 将支持适用于 WAN 驱动程序的未来 NDIS 增强功能。

 

