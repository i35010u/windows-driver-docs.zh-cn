---
title: NDIS 6.20 中的接收端限制
description: NDIS 6.20 中的接收端限制
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK，接收方限制
- 接收方限制 (RST) WDK NDIS 6.20
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26e8c6c9feecd08ae7782d825b013b23674b5c6e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211609"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 中的接收端限制





NDIS 6.20 引入了接收方限制 (RST) 增强功能，降低了在多媒体应用程序中播放媒体的过程中发生中断的可能性。 对于 NDIS 6.20 和更高版本的驱动程序，RST 支持是必需的。

如果 NDIS 驱动程序在延迟过程调用 (DPC) 中花费了太多的时间，则会增加多媒体应用程序线程的计划延迟时间，并可能导致媒体播放期间中断。 为了改进使用 NDIS 6.20 和更高版本驱动程序的媒体播放，NDIS 可以控制微型端口驱动程序在接收 DPC 中指示的数据包数。

## <a name="related-topics"></a>相关主题


[*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

[*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

[*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

[*MiniportMessageInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

[**NDIS \_ 接收 \_ 调节 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)

[**NdisMQueueDpcEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpcex)

 

