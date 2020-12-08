---
title: 协议驱动程序中的状态指示
description: 协议驱动程序中的状态指示
keywords:
- 协议驱动程序 WDK 网络，状态指示
- NDIS 协议驱动程序 WDK，状态指示
- 状态指示 WDK 网络，协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f0bae2124097d61dadc31feda6d017530610ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791345"
---
# <a name="status-indications-in-a-protocol-driver"></a>协议驱动程序中的状态指示





对于协议驱动程序中的状态指示，有两个不同的接口。 若要提供 [**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) 函数，需要一个具有无连接下限的 NDIS 协议驱动程序。 当基础无连接微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)来报告其硬件状态更改时，NDIS 将调用 *ProtocolStatusEx* 。 当状态更改开始时，NDIS 将调用 *ProtocolStatusEx* 。 有关无连接协议驱动程序中状态指示的详细信息，请参阅 [处理协议驱动程序中的状态指示](handling-status-indications-in-a-protocol-driver.md)。

面向连接的协议驱动程序必须提供 [**ProtocolCoStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex) 函数。 当面向连接的基础微型端口驱动程序调用 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)来报告其硬件状态更改时，NDIS 将调用 *ProtocolCoStatusEx* 。 当状态更改开始时，NDIS 将调用 *ProtocolCoStatusEx* 。 有关面向连接的协议驱动程序中状态指示的详细信息，请参阅 [面向连接的操作](connection-oriented-operations-performed-by-clients.md)

有关可能的状态指示的完整列表，请参阅 [状态指示](/windows-hardware/drivers/ddi/_netvista/)。

 

