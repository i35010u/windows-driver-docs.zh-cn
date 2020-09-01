---
title: 指示已从 CoNDIS WAN 微型端口驱动程序收到数据
description: 指示已从 CoNDIS WAN 微型端口驱动程序收到数据
ms.assetid: d49ea741-df5c-4b65-b899-a751cb2b9929
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，接收数据
- 接收数据 WDK 网络
- 指示 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec4cb461e6d600e044d82dccb8c3113f1e18995
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212425"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>指示已从 CoNDIS WAN 微型端口驱动程序收到数据





CoNDIS WAN 微型端口驱动程序收到网络数据包时，会发生以下操作：

1.  如果需要，驱动程序将从网络数据包中删除特定于驱动程序的封装，如有必要，然后调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists) 来指示网络 \_ 缓冲区列表结构中接收的数据 \_ 。 例如，驱动程序可以删除 PPPoE 封装。 但是，微型端口驱动程序应保留封装的数据，例如 PPP 标头和有效负载。

2.  驱动程序调用 **NdisMCoIndicateReceiveNetBufferLists** 函数，以指示 NDISWAN 数据包已到达。

3.  NDISWAN 处理数据包，并调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 来指示数据包到达。

4.  为了转发数据包，NDIS 调用了绑定的过量协议驱动程序的 [**ProtocolReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) 函数。

 

