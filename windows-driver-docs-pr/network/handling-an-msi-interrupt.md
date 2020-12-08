---
title: 处理 MSI 中断
description: 处理 MSI 中断
keywords:
- MSI-X WDK 网络，处理中断
- 消息-已发出信号中断 WDK 网络，处理中断
- Msi WDK 网络，处理中断
- 中断 WDK 网络，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc7eddb4041b392dab03bf6d7aad90d77dbec526
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788349"
---
# <a name="handling-an-msi-interrupt"></a>处理 MSI 中断





当网络接口卡 (NIC) 生成中断时，NDIS 将调用 [*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt) 函数。 此函数中的 *MessageId* 参数用于标识 MSI X 消息。

由于不共享消息中断，因此在处理中断后， *MiniportMessageInterrupt* 应始终返回 **TRUE** 。

小型小型驱动程序的 *MiniportMessageInterrupt* 函数中的工作应尽可能少。 驱动程序应将 i/o 操作延迟为 [*MiniportMessageInterruptDpc*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc) 函数，NDIS 调用该函数来完成中断的延迟处理。

若要在 [*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)返回后将其他延迟过程调用排队 (dpc) ，微型端口驱动程序将设置 *MiniportMessageInterrupt* 函数的 *TargetProcessors* 参数的位数。 若要从 *MiniportMessageInterrupt* 或 *MiniportMessageInterruptDPC* 请求其他 dpc，微型端口驱动程序可以调用 [**NdisMQueueDpc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpc) 函数。

微型端口驱动程序可以调用 **NdisMQueueDpc** 来请求其他处理器的其他 dpc。

NDIS 6.1 和更高版本保证为同一 CPU 计划的不同消息的 Dpc 单独排队。 例如，如果微型端口驱动程序在 CPU 1 上同时安排两个 Dpc (一个 DPC 用于消息0，另一个 dpc 用于消息 1) ，则会将两个 dpc 排队等候 CPU 1 (一个 DPC 包含消息0，另一个 dpc 使用消息 1) 。

NDIS 还保证在不同 Cpu 上计划的同一消息的 Dpc 单独排队。 例如，如果微型端口驱动程序将两个 dpc (一个 DPC 用于消息0，在 cpu 1 上的一个 DPC 上，对于消息 0) ，两个单独的 Dpc 在 CPU 0 和 CPU 1 上排队，同时用于消息0。

 

