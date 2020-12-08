---
title: AVStream 中的筛选器控件互斥
description: AVStream 中的筛选器控件互斥
keywords:
- 筛选器控件 mutex WDK AVStream
- AVStream mutex WDK
- mutex WDK AVStream
- 同步 WDK AVStream
- 状态转换 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10e01859337a99a3229189919be7e6328f4c438d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816497"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream 中的筛选器控件互斥





每个 AVStream 筛选器实例都有一个关联的筛选器控件互斥体。 此 mutex 用于同步从筛选器向下到各个 pin 的对象层次结构的访问。 创建和销毁筛选器和 pin 将与此 mutex 同步。

在持有筛选器控件互斥体时，对象层次结构保证 *只* 从特定筛选器实例稳定。 因此，微型驱动程序必须先获取筛选器控件互斥体，然后再使用 **Ks**_xxx_*_GetFirstChild_*_xxx_ 和 **ks**_xxx_*_GetNextSibling_*_xxx_ 函数遍历该筛选器级别下面的对象层次结构。

筛选器控件 mutex 还用于同步状态转换。

AVStream 在处理要求层次结构保持稳定的属性（例如在执行描述符修改时）时，将获取筛选器控件互斥体。

请注意，单个筛选器控件互斥体用于每个筛选器下的对象层次结构。 这意味着，当微型驱动程序调用带有固定对象的函数时，pin 对象将使用其父的筛选器控件互斥体。

当调用以下微型驱动程序提供的例程时，AVStream 代表微型驱动程序保存筛选器控件互斥体：

-   [*AVStrMiniFilterCreate*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterirp)

-   [*AVStrMiniFilterClose*](/previous-versions/ff556307(v=vs.85))

-   [*AVStrMiniPinCreate*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinirp)

-   [*AVStrMiniPinClose*](/previous-versions/ff556329(v=vs.85))

-   [*AVStrMiniPinConnect*](/previous-versions/ff556332(v=vs.85))

-   [*AVStrMiniPinDisconnect*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinvoid)

-   [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

-   [*AVStrMiniPinSetDeviceState*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)

与设备互斥体类似，不能以递归方式获取筛选器控件互斥体。 例如，如果 AVStream 在线程 A 的上下文中对 *Create* 调度发出了一个微型驱动程序的回调，并且该微型驱动程序稍后尝试从线程 a 中获取互斥体，则会将死锁与自身串接。

如果执行以下操作之一，则会发生死锁：

-   尝试从处理例程中获取筛选器控件互斥体。

-   尝试从睡眠或唤醒回调内获取筛选器控件互斥体。

若要操作筛选器控件互斥体，请使用以下函数：

[**KsAcquireControl**](/windows-hardware/drivers/ddi/ks/nf-ks-ksacquirecontrol)、 [**KsFilterAcquireControl**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilteracquirecontrol)、 [**KsPinAcquireControl**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquirecontrol)、 [**KsReleaseControl**](/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasecontrol)、 [**KsFilterReleaseControl**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterreleasecontrol)、 [**KsPinReleaseControl**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinreleasecontrol)

 

