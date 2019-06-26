---
title: 处理 MSI 中断
description: 处理 MSI 中断
ms.assetid: c8e2a5a4-17f5-48a3-a2d0-6eca2a0b7f45
keywords:
- MSI X WDK 连接网络、 处理中断
- 处理中断的消息信号中断 WDK 网络
- 处理中断的 Msi WDK 网络
- 中断 WDK 连接网络、 处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f813f43e7a715d1d76b89b4d14c576499169e1fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384398"
---
# <a name="handling-an-msi-interrupt"></a>处理 MSI 中断





NDIS 调用[ *MiniportMessageInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)函数时网络接口卡 (NIC) 会产生中断。 *MessageId*中此函数的参数标识 MSI X 的消息。

*MiniportMessageInterrupt*应始终返回**TRUE**之后处理中断，因为不共享消息中断。

微型端口驱动程序应执行尽可能少地尽可能在其*MiniportMessageInterrupt*函数。 该驱动程序应延迟到的 I/O 操作[ *MiniportMessageInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc)函数，NDIS 调用以完成延迟的处理的中断。

到其他队列延迟过程调用 (Dpc) 后[ *MiniportMessageInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)返回时，微型端口驱动程序设置的位*TargetProcessors*参数*MiniportMessageInterrupt*函数。 若要请求来自其他 Dpc *MiniportMessageInterrupt*或*MiniportMessageInterruptDPC*，微型端口驱动程序可以调用[ **NdisMQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueuedpc)函数。

微型端口驱动程序可以调用**NdisMQueueDpc**来请求更多其他处理器的 dpc 进行标记。

NDIS 6.1 和更高版本将保证 Dpc 的计划进行单独排队同一个 CPU 的不同消息。 例如，如果微型端口驱动程序同时在 CPU 1 （一个 DPC 消息 0 和消息 1 其他 DPC） 上安排两个 Dpc，两个 Dpc 排队等待 CPU 1 (一个 DPC 消息 0) 和其他 DPC 与第一条消息。

NDIS 还可确保不同的 Cpu 计划针对同一邮件 Dpc 排队单独。 例如，如果微型端口驱动程序安排两个 Dpc (一个 DPC 上 CPU 消息 0 0) 和一个 DPC 消息 0 的 CPU 1 上时，两个单独 Dpc 将排队 CPU 0 和 CPU 1，同时用于消息 0 上。

 

 





