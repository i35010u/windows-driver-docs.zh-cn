---
title: 筛选器控件中 AVStream 的互斥体
description: 筛选器控件中 AVStream 的互斥体
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- 筛选器控件互斥体 WDK AVStream
- AVStream 互斥体 WDK
- 互斥体，WDK AVStream
- 同步 WDK AVStream
- 状态转换 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06a6af77bfa218d18fc6dab43c4f5c9b1d342d84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520571"
---
# <a name="filter-control-mutex-in-avstream"></a>筛选器控件中 AVStream 的互斥体





每个 AVStream 筛选器实例都有关联的筛选器控件互斥体。 使用此互斥体的访问进行同步的对象层次结构从筛选器向下拖动到各个 pin。 与此互斥体同步筛选器和 pin 的创建和析构。

保证对象层次结构是稳定*仅*互斥体持有从特定筛选器时，实例向下筛选器控件。 相应地，微型驱动程序必须遍历下筛选器级别使用的对象层次结构之前获取筛选器控件互斥体 **Ks***Xxx***GetFirstChild * * * Xxx*和 **Ks***Xxx***GetNextSibling * * * Xxx*函数。

筛选器控件互斥体也用于同步状态转换。

当处理需要层次结构，以保持稳定，例如，当执行描述符修改的属性时，AVStream 获取筛选器控件互斥体。

请注意，单个筛选器控件互斥体用于下每个单独的筛选器的对象层次结构。 这意味着 pin 对象使用其父项的筛选器控件互斥体，微型驱动程序调用的函数与 pin 对象时。

AVStream 代表微型驱动程序保存筛选器控件互斥体时调用以下微型驱动程序提供的例程：

-   [*AVStrMiniFilterCreate*](https://msdn.microsoft.com/library/windows/hardware/ff556310)

-   [*AVStrMiniFilterClose*](https://msdn.microsoft.com/library/windows/hardware/ff556307)

-   [*AVStrMiniPinCreate*](https://msdn.microsoft.com/library/windows/hardware/ff556334)

-   [*AVStrMiniPinClose*](https://msdn.microsoft.com/library/windows/hardware/ff556329)

-   [*AVStrMiniPinConnect*](https://msdn.microsoft.com/library/windows/hardware/ff556332)

-   [*AVStrMiniPinDisconnect*](https://msdn.microsoft.com/library/windows/hardware/ff556337)

-   [*AVStrMiniPinSetDataFormat*](https://msdn.microsoft.com/library/windows/hardware/ff556355)

-   [*AVStrMiniPinSetDeviceState*](https://msdn.microsoft.com/library/windows/hardware/ff556359)

类似于设备互斥体，筛选器控件互斥体必须获得以递归方式。 如果，例如，AVStream 对回调的微型驱动程序*创建*调度线程 A，在上下文和微型驱动程序中更高版本尝试获取互斥体从一个线程内的，线程 A 与其自身的死锁。

如果您执行以下操作之一，则会发生死锁：

-   尝试获取进程例程中的从筛选器控件互斥体。

-   尝试获取中的从该筛选器控件互斥体的睡眠或唤醒回调。

若要操作筛选器控件互斥体，使用以下函数：

[**KsAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff560908)， [ **KsFilterAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff562523)， [ **KsPinAcquireControl**](https://msdn.microsoft.com/library/windows/hardware/ff563485)， [**KsReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff566780)， [ **KsFilterReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff562551)， [ **KsPinReleaseControl**](https://msdn.microsoft.com/library/windows/hardware/ff563526)

 

 




