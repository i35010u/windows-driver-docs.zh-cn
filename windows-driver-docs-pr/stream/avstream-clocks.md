---
title: AVStream 时钟
description: AVStream 时钟
ms.assetid: fc1d5bca-72e3-48e2-b46f-09a13bba83b4
keywords:
- 时钟 WDK AVStream
- AVStream 时钟 WDK
- 将固定时钟 WDK AVStream
- 计时器 WDK AVStream
- 时间 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 344d17361e2285904d85335e53d89f9622b9b98a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352699"
---
# <a name="avstream-clocks"></a>AVStream 时钟





AVStream 筛选器支持插针上的时钟。

若要指示 AVStream pin 公开一个时钟，设置 KSPIN\_标志\_实现\_的时钟**标志**的第一个成员[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)中**PinDescriptors**隶属[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553).

此外提供了一个指向[ **KSCLOCK\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff561017)结构[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)。

若要使时钟的请求，请使用上定义的方法[IKsReferenceClock](https://msdn.microsoft.com/library/windows/hardware/ff560725)接口。 你可以获得*IKsReferenceClock*接口通过调用[ **KsPinGetReferenceClockInterface**](https://msdn.microsoft.com/library/windows/hardware/ff563517)。 AVStream 微型驱动程序会释放接口完成。

若要获取计时器值置于**PresentationTime**字段[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)，调用[ **IKsReferenceClock::GetCorrelatedTime**](https://msdn.microsoft.com/library/windows/hardware/ff560728)。

请注意，时钟永远不会出现在 GraphEdit，即使已选择时钟。

若要验证是否已选中时钟，请验证的调用[IKsReferenceClock](https://msdn.microsoft.com/library/windows/hardware/ff560725)方法生成一些调用来调度 KSCLOCK 中指定的例程\_调度。

筛选器图形管理器选择时钟时关系图将转为暂停状态。 是推送源，例如使用捕获筛选器，任何筛选器作为时钟提供程序提供首选项。

 

 




