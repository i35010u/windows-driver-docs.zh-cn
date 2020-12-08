---
title: AVStream 时钟
description: AVStream 时钟
keywords:
- 时钟 WDK AVStream
- AVStream 时钟 WDK
- 固定时钟 WDK AVStream
- 计时器 WDK AVStream
- 时间 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3a7eaf5fe20822cf1cf4507fe969988e73d97d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815841"
---
# <a name="avstream-clocks"></a>AVStream 时钟





AVStream 筛选器支持对 pin 进行时钟。

若要指示 AVStream pin 公开了时钟，请 \_ \_ \_ 在第一个 KSPIN 说明符的 **Flags** 成员（ [**\_ \_ 例如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)的 **PinDescriptors** 成员中）设置 KSPIN 标记实现时钟。

还提供指向 [**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)中的 [**KSCLOCK \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksclock_dispatch)结构的指针。

若要发出时钟请求，请使用 [IKsReferenceClock](/windows-hardware/drivers/ddi/ks/nn-ks-iksreferenceclock) 接口上定义的方法。 可以通过调用 [**KsPinGetReferenceClockInterface**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetreferenceclockinterface)获取 *IKsReferenceClock* 接口。 AVStream 微型驱动程序负责在完成时释放接口。

若要获取要放置在 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)的 **PresentationTime** 字段中的计时器值，请调用 [**IKsReferenceClock：： GetCorrelatedTime**](/windows-hardware/drivers/ddi/ks/nf-ks-iksreferenceclock-getcorrelatedtime)。

请注意，即使已选择时钟，时钟也永远不会显示在 GraphEdit 中。

若要验证是否已选择时钟，请验证对 [IKsReferenceClock](/windows-hardware/drivers/ddi/ks/nn-ks-iksreferenceclock) 方法的调用是否生成对 KSCLOCK 调度中指定的调度例程的调用 \_ 。

当图形转换到暂停状态时，筛选器图形管理器会选择时钟。 作为 "捕获筛选器" 的任何作为推送源的筛选器都优先于 "时钟提供程序"。

 

