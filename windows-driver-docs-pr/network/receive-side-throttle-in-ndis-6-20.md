---
title: NDIS 6.20 中的接收端限制
description: NDIS 6.20 中的接收端限制
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK，接收方限制
- 接收端限制 (RST) WDK NDIS 6.20
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a8e167454faf586344151b63fadfa5179ef2d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373325"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 中的接收端限制





NDIS 6.20 引入了接收端限制 (RST) 增强功能，若要在多媒体应用程序中的媒体播放期间降低中断的可能性。 RST 的支持是必需的 NDIS 6.20 和更高版本的驱动程序。

如果 NDIS 驱动程序花费在调度延迟的过程调用 (DPC) 中的 IRQ 级别太多时间，这可以增加多媒体应用程序线程的调度延迟时间并可能会导致中断期间播放媒体。 若要提高使用 NDIS 6.20 和更高版本的驱动程序媒体播放，NDIS 可以控制在接收 DPC 中指示的微型端口驱动程序的数据包数。

## <a name="related-topics"></a>相关主题


[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)

[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)

[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)

[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc)

[**NDIS\_RECEIVE\_THROTTLE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_throttle_parameters)

[**NdisMQueueDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueuedpcex)

 

 






