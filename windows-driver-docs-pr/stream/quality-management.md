---
title: 质量管理
description: 质量管理
ms.assetid: 359e6e12-903f-4037-8f35-b090ce41f770
keywords:
- 质量管理 WDK 内核流式处理
- KSPROPERTY_STREAM_QUALITY
- KSQUALITY_MANAGER
- 通知 WDK 内核流式处理
- 投诉 WDK 内核流式处理
- 内核流 WDK，质量管理
- KS WDK，质量管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4ee37d46bcd13adc6ac8b2f12585a6fc62bae0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841663"
---
# <a name="quality-management"></a>质量管理





内核流式处理体系结构提供了对质量管理的可选支持。 此机制调整流控制以匹配资源约束，并确定筛选器图中的需求下降。 质量管理通知通过内核模式代理来发送。

报告质量管理问题的 pin 支持[**KSPROPERTY\_流\_质量**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-quality)属性。 这是一个可选的只写属性，pin 可将该属性设置为 QM 投诉接收器的句柄和上下文参数。 为此，pin 提供了包含此信息的[**KSQUALITY\_管理器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)类型的结构。 Pin 连接反过来使用此信息，通过具有给定上下文参数的[**KSQUALITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)结构通知质量管理器的问题。

为允许用户模式客户端提交质量管理投诉，微型驱动程序支持 KSPROPSETID 中的属性[\_质量](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-quality)。

如果 pin 允许降低策略，则微型驱动程序支持[**KSPROPERTY\_流\_降级**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-degradation)属性。

有关详细信息，请参阅[**KSDEGRADE**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85)) and [**KSDEGRADE\_STANDARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksdegrade_standard)。

 

 




