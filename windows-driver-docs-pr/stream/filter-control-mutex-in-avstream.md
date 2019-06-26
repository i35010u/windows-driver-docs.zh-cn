---
title: AVStream 中的筛选器控件互斥
description: AVStream 中的筛选器控件互斥
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- 筛选器控件互斥体 WDK AVStream
- AVStream 互斥体 WDK
- 互斥体，WDK AVStream
- 同步 WDK AVStream
- 状态转换 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4372cc34cb959dc3431b5c2fabc358eced0ee528
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384062"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream 中的筛选器控件互斥





每个 AVStream 筛选器实例都有关联的筛选器控件互斥体。 使用此互斥体的访问进行同步的对象层次结构从筛选器向下拖动到各个 pin。 与此互斥体同步筛选器和 pin 的创建和析构。

保证对象层次结构是稳定*仅*互斥体持有从特定筛选器时，实例向下筛选器控件。 相应地，微型驱动程序必须遍历下筛选器级别使用的对象层次结构之前获取筛选器控件互斥体 **Ks***Xxx***GetFirstChild * * * Xxx*和 **Ks***Xxx***GetNextSibling * * * Xxx*函数。

筛选器控件互斥体也用于同步状态转换。

当处理需要层次结构，以保持稳定，例如，当执行描述符修改的属性时，AVStream 获取筛选器控件互斥体。

请注意，单个筛选器控件互斥体用于下每个单独的筛选器的对象层次结构。 这意味着 pin 对象使用其父项的筛选器控件互斥体，微型驱动程序调用的函数与 pin 对象时。

AVStream 代表微型驱动程序保存筛选器控件互斥体时调用以下微型驱动程序提供的例程：

-   [*AVStrMiniFilterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterirp)

-   [*AVStrMiniFilterClose*](https://docs.microsoft.com/previous-versions/ff556307(v=vs.85))

-   [*AVStrMiniPinCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinirp)

-   [*AVStrMiniPinClose*](https://docs.microsoft.com/previous-versions/ff556329(v=vs.85))

-   [*AVStrMiniPinConnect*](https://docs.microsoft.com/previous-versions/ff556332(v=vs.85))

-   [*AVStrMiniPinDisconnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinvoid)

-   [*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdataformat)

-   [*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)

类似于设备互斥体，筛选器控件互斥体必须获得以递归方式。 如果，例如，AVStream 对回调的微型驱动程序*创建*调度线程 A，在上下文和微型驱动程序中更高版本尝试获取互斥体从一个线程内的，线程 A 与其自身的死锁。

如果您执行以下操作之一，则会发生死锁：

-   尝试获取进程例程中的从筛选器控件互斥体。

-   尝试获取中的从该筛选器控件互斥体的睡眠或唤醒回调。

若要操作筛选器控件互斥体，使用以下函数：

[**KsAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquirecontrol)， [ **KsFilterAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilteracquirecontrol)， [ **KsPinAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinacquirecontrol)， [**KsReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasecontrol)， [ **KsFilterReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterreleasecontrol)， [ **KsPinReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinreleasecontrol)

 

 




