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
ms.openlocfilehash: 2e36610b937f19664b53cc33ecfef15582e82edc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824633"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>指示已从 CoNDIS WAN 微型端口驱动程序收到数据





CoNDIS WAN 微型端口驱动程序收到网络数据包时，会发生以下操作：

1.  如果需要，驱动程序将在调用[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)以指示网络\_缓冲区\_列表结构中收到的数据之前，从网络数据包中删除特定于驱动程序的封装。 例如，驱动程序可以删除 PPPoE 封装。 但是，微型端口驱动程序应保留封装的数据，例如 PPP 标头和有效负载。

2.  驱动程序调用**NdisMCoIndicateReceiveNetBufferLists**函数，以指示 NDISWAN 数据包已到达。

3.  NDISWAN 处理数据包，并调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)来指示数据包到达。

4.  为了转发数据包，NDIS 调用了绑定的过量协议驱动程序的[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数。

 

 





