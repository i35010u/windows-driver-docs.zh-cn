---
title: NDIS 6.20 中的接收端限制
description: NDIS 6.20 中的接收端限制
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK，接收方限制
- 接收方限制（RST） WDK NDIS 6.20
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6287e1f7c4a87d542feacf7878098c834b365884
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844858"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 中的接收端限制





NDIS 6.20 引入了接收端限制（RST）增强功能，以减少在多媒体应用程序中播放媒体的过程中发生中断的可能性。 对于 NDIS 6.20 和更高版本的驱动程序，RST 支持是必需的。

如果 NDIS 驱动程序在延迟的过程调用（DPC）的调度 IRQ 级别花费了太多的时间，则会增加多媒体应用程序线程的计划延迟时间，并可能导致媒体播放期间中断。 为了改进使用 NDIS 6.20 和更高版本驱动程序的媒体播放，NDIS 可以控制微型端口驱动程序在接收 DPC 中指示的数据包数。

## <a name="related-topics"></a>相关主题


[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

[**NDIS\_接收\_控制器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)

[**NdisMQueueDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpcex)

 

 






