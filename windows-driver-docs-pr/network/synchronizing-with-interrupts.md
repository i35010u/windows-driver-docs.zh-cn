---
title: 与中断同步
description: 与中断同步
keywords:
- 中断 WDK 网络，同步
- NdisMSynchronizeWithInterruptEx
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e451aa128207aed0e1ce1cc701262288721e289e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831225"
---
# <a name="synchronizing-with-interrupts"></a>与中断同步





如果微型端口驱动程序的 [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数与另一个 MiniportXxx 函数共享资源（如 NIC 寄存器或状态变量），而另一个 *MiniportXxx* 函数在较低的 IRQL 运行，则 *MiniportXxx* 函数必须调用 [**NdisMSynchronizeWithInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)。 此调用可确保微型端口驱动程序的 [*MiniportSynchronizeInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt) 函数以同步且多处理器安全的方式访问共享资源。

 

