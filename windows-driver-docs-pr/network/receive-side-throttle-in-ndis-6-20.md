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
ms.openlocfilehash: f753335a06a4592e407b92503803623a664d7a0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353326"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 中的接收端限制





NDIS 6.20 引入了接收端限制 (RST) 增强功能，若要在多媒体应用程序中的媒体播放期间降低中断的可能性。 RST 的支持是必需的 NDIS 6.20 和更高版本的驱动程序。

如果 NDIS 驱动程序花费在调度延迟的过程调用 (DPC) 中的 IRQ 级别太多时间，这可以增加多媒体应用程序线程的调度延迟时间并可能会导致中断期间播放媒体。 若要提高使用 NDIS 6.20 和更高版本的驱动程序媒体播放，NDIS 可以控制在接收 DPC 中指示的微型端口驱动程序的数据包数。

## <a name="related-topics"></a>相关主题


[*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)

[*MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)

[*MiniportMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559407)

[*MiniportMessageInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559411)

[**NDIS\_RECEIVE\_THROTTLE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567241)

[**NdisMQueueDpcEx**](https://msdn.microsoft.com/library/windows/hardware/ff563640)

 

 






