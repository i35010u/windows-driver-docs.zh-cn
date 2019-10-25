---
title: 协议驱动程序中的状态指示
description: 协议驱动程序中的状态指示
ms.assetid: 4b0426bb-4311-4251-b9ee-38d081f061e5
keywords:
- 协议驱动程序 WDK 网络，状态指示
- NDIS 协议驱动程序 WDK，状态指示
- 状态指示 WDK 网络，协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e97189ff0ab5733b51d7897897dfdca610651bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841826"
---
# <a name="status-indications-in-a-protocol-driver"></a>协议驱动程序中的状态指示





对于协议驱动程序中的状态指示，有两个不同的接口。 若要提供[**ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)函数，需要一个具有无连接下限的 NDIS 协议驱动程序。 当基础无连接微型端口驱动程序调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)来报告其硬件状态更改时，NDIS 将调用*ProtocolStatusEx* 。 当状态更改开始时，NDIS 将调用*ProtocolStatusEx* 。 有关无连接协议驱动程序中状态指示的详细信息，请参阅[处理协议驱动程序中的状态指示](handling-status-indications-in-a-protocol-driver.md)。

面向连接的协议驱动程序必须提供[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)函数。 当面向连接的基础微型端口驱动程序调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)来报告其硬件状态更改时，NDIS 将调用*ProtocolCoStatusEx* 。 当状态更改开始时，NDIS 将调用*ProtocolCoStatusEx* 。 有关面向连接的协议驱动程序中状态指示的详细信息，请参阅[面向连接的操作](connection-oriented-operations.md)

有关可能的状态指示的完整列表，请参阅[状态指示](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 





