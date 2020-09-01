---
title: 处理 NDIS 微型端口驱动程序的中断
description: 讨论当 NIC 或其他设备生成中断时 NDIS 微型端口驱动程序使用的调用
ms.assetid: 75dc3676-f88f-4d86-8c77-02f48083de71
keywords:
- 中断 WDK 网络，处理
- MiniportInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3eaf9ed6160e28cd54ccc7d7a376a7e871e6a7f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215867"
---
# <a name="handling-interrupts-for-ndis-miniport-drivers"></a>处理 NDIS 微型端口驱动程序的中断





当 NIC 或与 NIC 共享中断的另一台设备生成中断时，NDIS 将调用 [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr) 函数。

如果基础 NIC 不生成中断， *MiniportInterrupt*应立即返回**FALSE** 。 否则，在处理中断后，它将返回 **TRUE** 。

小型小型驱动程序的 *MiniportInterrupt* 函数中的工作应尽可能少。 它应将 i/o 操作延迟到 [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc) 函数中。 NDIS 调用 *MiniportInterruptDPC* 来完成中断的延迟处理。

若要在*MiniportInterrupt*返回后将其他 dpc 排队，微型端口驱动程序将设置*MiniportInterrupt*函数的[**TargetProcessors**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpc)参数的位数。 若要从 *MiniportInterrupt* 或 *MiniportInterruptDPC*请求其他 dpc，微型端口驱动程序调用 **NdisMQueueDpc** 函数。

微型端口驱动程序可以调用 **NdisMQueueDpc** 来请求其他处理器的其他 DPC 调用。

 

