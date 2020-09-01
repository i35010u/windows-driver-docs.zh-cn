---
title: 与中断同步
description: 与中断同步
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- 中断 WDK 网络，同步
- NdisMSynchronizeWithInterruptEx
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50ab2afc7042c1c5525fb27aedb4b77abc626aa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207147"
---
# <a name="synchronizing-with-interrupts"></a>与中断同步





如果微型端口驱动程序的[*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数与另一个 MiniportXxx 函数共享资源（如 NIC 寄存器或状态变量），而另一个*MiniportXxx*函数在较低的 IRQL 运行，则*MiniportXxx*函数必须调用[**NdisMSynchronizeWithInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)。 此调用可确保微型端口驱动程序的 [*MiniportSynchronizeInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt) 函数以同步且多处理器安全的方式访问共享资源。

 

