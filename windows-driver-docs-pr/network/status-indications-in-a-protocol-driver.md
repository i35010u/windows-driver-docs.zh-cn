---
title: 协议驱动程序中的状态指示
description: 协议驱动程序中的状态指示
ms.assetid: 4b0426bb-4311-4251-b9ee-38d081f061e5
keywords:
- 协议驱动程序 WDK 网络状态指示
- NDIS 协议驱动程序 WDK，状态指示
- 状态指示 WDK 网络协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae9fc25de2fb70e9313b1037cbae106525f057e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383610"
---
# <a name="status-indications-in-a-protocol-driver"></a>协议驱动程序中的状态指示





有两个不同接口的状态指示在协议驱动程序。 无连接的下边缘与的 NDIS 协议驱动程序需要提供[ **ProtocolStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)函数。 NDIS 调用*ProtocolStatusEx*当基础的无连接的微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)来报告其硬件状态中的更改。 NDIS 调用*ProtocolStatusEx*开始的状态更改时。 有关状态指示无连接协议驱动程序中的详细信息，请参阅[协议驱动程序中处理状态指示](handling-status-indications-in-a-protocol-driver.md)。

面向连接的协议驱动程序必须提供[ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)函数。 NDIS 调用*ProtocolCoStatusEx*当基础的面向连接的微型端口驱动程序调用[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)来报告其硬件状态中的更改. NDIS 调用*ProtocolCoStatusEx*开始的状态更改时。 有关在面向连接的协议驱动程序中的状态指示的详细信息，请参阅[Connection-Oriented 操作](connection-oriented-operations.md)

有关可能的状态指示的完整列表，请参阅[状态指示](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

 

 





