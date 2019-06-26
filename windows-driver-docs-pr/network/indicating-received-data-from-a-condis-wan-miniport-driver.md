---
title: 指示已从 CoNDIS WAN 微型端口驱动程序收到数据
description: 指示已从 CoNDIS WAN 微型端口驱动程序收到数据
ms.assetid: d49ea741-df5c-4b65-b899-a751cb2b9929
keywords:
- CoNDIS WAN 的驱动程序 WDK 网络接收数据
- 接收数据 WDK 网络
- 指示 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf90153d19af7a177a0fc67c123a2e85993ebc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380899"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>指示已从 CoNDIS WAN 微型端口驱动程序收到数据





当 CoNDIS WAN 的微型端口驱动程序收到网络数据包时，将发生以下操作：

1.  该驱动程序从中删除特定于驱动程序封装网络数据包，如有必要，然后再调用[ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)以指示接收到的数据在 NET\_缓冲区\_列表结构。 例如，驱动程序可以删除 PPPoE 封装。 但是，微型端口驱动程序应将封装的数据，如 PPP 标头和有效负载，保持不变。

2.  驱动程序调用**NdisMCoIndicateReceiveNetBufferLists**函数来指示到 NDISWAN 的数据包到达。

3.  NDISWAN 处理数据包并调用[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)以指示何时到达该数据包。

4.  若要转发的数据包、 NDIS 调用[ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)绑定基础协议驱动程序的函数。

 

 





