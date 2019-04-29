---
title: AVStream 中的设备互斥
description: AVStream 中的设备互斥
ms.assetid: cec2a040-59d6-44ef-aef1-04f434811d60
keywords:
- AVStream 互斥体 WDK
- 互斥体，WDK AVStream
- 设备互斥体 WDK AVStream
- 同步 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076849ef6bfbb21aafd6be5f60750e6ff57f1139
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374053"
---
# <a name="device-mutex-in-avstream"></a>AVStream 中的设备互斥





使用设备互斥体同步从设备到筛选器层次结构中的对象。 每个 AVStream 设备都有一个关联的设备互斥体。 创建和销毁这两者的筛选器工厂和与此互斥体同步筛选器。 某些插和电源管理操作也会使用此互斥体同步。 微型驱动程序重点介绍有关设备互斥体的两个主要问题。

保证对象层次结构是稳定*仅*从设备到单个筛选器，如果设备互斥锁被保留。 因此，微型驱动程序必须手动创建筛选器工厂通过调用之前获取设备 mutex [ **KsCreateFilterFactory**](https://msdn.microsoft.com/library/windows/hardware/ff561650)。 微型驱动程序还必须通过调用遍历对象层次结构之前获取设备互斥体 **Ks***Xxx***GetFirstChild * * * Xxx*和 **Ks***Xxx***GetNextSibling * * * Xxx*函数。

AVStream 代表微型驱动程序保存设备互斥体时接收以下请求：

-   [**IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)

-   [**IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)

-   [*PostStart 调度*](https://msdn.microsoft.com/library/windows/hardware/ff554284)

-   [**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

-   [**IRP\_MN\_查询\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)

-   [**IRP\_MN\_SET\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)

-   睡眠和唤醒通知筛选器和 pin。 请参阅[ **KsFilterRegisterPowerCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff562550)并[ **KsPinRegisterPowerCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff563525)。

请务必注意，不能获得设备互斥体以递归方式。 请考虑下面的示例。 AVStream 接收睡眠状态通知。 如上所述，代表微型驱动程序需要设备互斥体。 如果 AVStream 然后在线程 A 的上下文中调用微型驱动程序提供的回调例程，微型驱动程序必须随后尝试获取设备互斥体，因此 A.执行与其自身将导致死锁的线程 A 的线程中。

AVStream 通常获取互斥体，筛选器控件，当设备互斥体已被占用。 因此，作为一般规则，已筛选器控件 mutex 的线程随后不应带有设备互斥体。

若要操作设备互斥体，使用以下函数：

[**KsAcquireDevice**](https://msdn.microsoft.com/library/windows/hardware/ff560911)， [ **KsReleaseDevice**](https://msdn.microsoft.com/library/windows/hardware/ff566783)

 

 




