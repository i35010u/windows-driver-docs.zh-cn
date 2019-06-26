---
title: 质量管理
description: 质量管理
ms.assetid: 359e6e12-903f-4037-8f35-b090ce41f770
keywords:
- 质量管理 WDK 内核流式处理
- KSPROPERTY_STREAM_QUALITY
- KSQUALITY_MANAGER
- 通知 WDK 内核流式处理
- 流式处理的投诉 WDK 内核
- 内核流式处理 WDK、 质量管理
- KS WDK、 质量管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd514deeb1f421bb4fc7a4523db04ecd08366bc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385686"
---
# <a name="quality-management"></a>质量管理





内核流式处理体系结构为质量管理提供的可选支持。 此机制调整流控制，以匹配资源约束，并确定筛选器关系图中的性能降低需求。 通过内核模式代理发送质量管理通知。

报告质量管理问题的支持的插针[ **KSPROPERTY\_流\_质量**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-quality)属性。 这是可选的只写属性，pin 可以设置为 QM 投诉接收器的句柄和上下文参数。 若要执行此操作，pin，提供了类型的结构[ **KSQUALITY\_MANAGER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality_manager) ，其中包含此信息。 Pin 连接又使用此信息以通知使用时出现问题的质量管理器[ **KSQUALITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksquality)具有给定的上下文参数的结构。

若要允许用户模式下客户端提交质量管理抱怨，微型驱动程序支持中的属性[KSPROPSETID\_质量](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-quality)。

如果 pin 允许下降策略，微型驱动程序支持[ **KSPROPERTY\_流\_下降**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-degradation)属性。

有关详细信息，请参阅[ **KSDEGRADE** ](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))并[ **KSDEGRADE\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksdegrade_standard)。

 

 




