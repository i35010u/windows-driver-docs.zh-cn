---
title: 与中断同步
description: 与中断同步
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- 中断 WDK 网络同步
- NdisMSynchronizeWithInterruptEx
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb23cd578eea16a0e1ab99807cc44ef8088402ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377951"
---
# <a name="synchronizing-with-interrupts"></a>与中断同步





如果微型端口驱动程序[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)函数与另一个共享资源，例如 NIC 寄存器或状态变量*MiniportXxx*在运行的函数降低 irql，因此， *MiniportXxx*函数必须调用[ **NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsynchronizewithinterruptex)。 此调用可确保微型端口驱动程序[ *MiniportSynchronizeInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_synchronize_interrupt)函数同步且包含多个处理器安全的方式可以访问共享的资源。

 

 





