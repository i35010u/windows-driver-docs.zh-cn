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
ms.openlocfilehash: b1112beabeee0241c590cf4a2ced87effc5022e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841785"
---
# <a name="synchronizing-with-interrupts"></a>与中断同步





如果微型端口驱动程序的[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数与另一个 MiniportXxx 函数共享资源（如 NIC 寄存器或状态变量），而另一个函数在较低的 IRQL 运行，则*MiniportXxx*函数必须调用[**NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)。 此调用可确保微型端口驱动程序的[*MiniportSynchronizeInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt)函数以同步且多处理器安全的方式访问共享资源。

 

 





