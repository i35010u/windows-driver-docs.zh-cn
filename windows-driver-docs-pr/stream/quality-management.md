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
ms.openlocfilehash: d70757621730b3f53ebc0cd854ab3894fc7295f7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188000"
---
# <a name="quality-management"></a>质量管理





内核流式处理体系结构提供了对质量管理的可选支持。 此机制调整流控制以匹配资源约束，并确定筛选器图中的需求下降。 质量管理通知通过内核模式代理来发送。

报表质量管理问题的 pin 支持 [**KSPROPERTY \_ 流 \_ 质量**](./ksproperty-stream-quality.md) 属性。 这是一个可选的只写属性，pin 可将该属性设置为 QM 投诉接收器的句柄和上下文参数。 为此，pin 提供了包含此信息的 [**KSQUALITY \_ MANAGER**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager) 类型的结构。 Pin 连接反过来使用此信息，通过具有给定上下文参数的 [**KSQUALITY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksquality) 结构通知质量管理器的问题。

若要允许用户模式客户端提交质量管理投诉，微型驱动程序支持 [KSPROPSETID \_ 质量](./kspropsetid-quality.md)属性。

如果 pin 允许降低策略，则微型驱动程序支持 [**KSPROPERTY \_ 流 \_ 降级**](./ksproperty-stream-degradation.md) 属性。

有关详细信息，请参阅 [**KSDEGRADE**](/previous-versions/ff561671(v=vs.85)) 和 [**KSDEGRADE \_ STANDARD**](/windows-hardware/drivers/ddi/ks/ne-ks-ksdegrade_standard)。

 

