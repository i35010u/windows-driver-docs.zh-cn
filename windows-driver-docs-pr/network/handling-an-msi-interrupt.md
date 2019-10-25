---
title: 处理 MSI 中断
description: 处理 MSI 中断
ms.assetid: c8e2a5a4-17f5-48a3-a2d0-6eca2a0b7f45
keywords:
- MSI-X WDK 网络，处理中断
- 消息-已发出信号中断 WDK 网络，处理中断
- Msi WDK 网络，处理中断
- 中断 WDK 网络，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72a8b3c29b99cf6887595bc7cc1176dc40345d88
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840478"
---
# <a name="handling-an-msi-interrupt"></a>处理 MSI 中断





当网络接口卡（NIC）生成中断时，NDIS 将调用[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)函数。 此函数中的*MessageId*参数用于标识 MSI X 消息。

由于不共享消息中断，因此在处理中断后， *MiniportMessageInterrupt*应始终返回**TRUE** 。

小型小型驱动程序的*MiniportMessageInterrupt*函数中的工作应尽可能少。 驱动程序应将 i/o 操作延迟为[*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)函数，NDIS 调用该函数来完成中断的延迟处理。

若要在[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)返回后将其他延迟的过程调用（dpc）排队，微型端口驱动程序将设置*MiniportMessageInterrupt*函数的*TargetProcessors*参数的位数。 若要从*MiniportMessageInterrupt*或*MiniportMessageInterruptDPC*请求其他 dpc，微型端口驱动程序可以调用[**NdisMQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpc)函数。

微型端口驱动程序可以调用**NdisMQueueDpc**来请求其他处理器的其他 dpc。

NDIS 6.1 和更高版本保证为同一 CPU 计划的不同消息的 Dpc 单独排队。 例如，如果小型端口驱动程序在 CPU 1 上同时安排两个 Dpc （一个 DPC 用于消息0，另一个 dpc 用于消息1），则两个 Dpc 将排队等待 CPU 1 （一个 DPC 带有消息0，另一个 dpc 带有消息1）。

NDIS 还保证在不同 Cpu 上计划的同一消息的 Dpc 单独排队。 例如，如果微型端口驱动程序计划两个 Dpc （CPU 0 上的一个 DPC 用于消息0，1个 dpc 位于 cpu 1 上，用于消息0），则两个单独的 Dpc 在 CPU 0 和 CPU 1 上排队，同时用于消息0。

 

 





