---
title: 处理中断的 NDIS 微型端口驱动程序
description: 讨论当 NIC 时，使用 NDIS 微型端口驱动程序或另一台设备生成中断的调用
ms.assetid: 75dc3676-f88f-4d86-8c77-02f48083de71
keywords:
- 中断 WDK 连接网络、 处理
- MiniportInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0dc90a92505324ac6800c8ed3a7186153667f45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379823"
---
# <a name="handling-interrupts-for-ndis-miniport-drivers"></a>处理中断的 NDIS 微型端口驱动程序





NDIS 调用[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr) NIC 或 NIC，请与共享中断的另一台设备生成中断时的功能。

*MiniportInterrupt*应返回**FALSE**立即如果基础 NIC 未生成中断。 否则，它将返回 **，则返回 TRUE**之后处理中断。

微型端口驱动程序应执行尽可能少地尽可能在其*MiniportInterrupt*函数。 它应延迟到的 I/O 操作[ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)函数。 NDIS 调用*MiniportInterruptDPC*完成延迟的处理的中断。

若要进行排队后的附加 Dpc *MiniportInterrupt*返回时，微型端口驱动程序设置的位[ **TargetProcessors** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueuedpc)参数*MiniportInterrupt*函数。 若要请求来自其他 Dpc *MiniportInterrupt*或*MiniportInterruptDPC*，微型端口驱动程序调用**NdisMQueueDpc**函数。

微型端口驱动程序可以调用**NdisMQueueDpc**以请求其他 DPC 调用其他处理器。

 

 





