---
title: AVStream 中的设备互斥
description: AVStream 中的设备互斥
keywords:
- AVStream mutex WDK
- mutex WDK AVStream
- 设备 mutex WDK AVStream
- 同步 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9778053a9e753c1ad35dedcb1231eab70b785b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830887"
---
# <a name="device-mutex-in-avstream"></a>AVStream 中的设备互斥





使用设备 mutex 将层次结构中的对象从设备向下同步到筛选器。 每个 AVStream 设备都有一个关联的设备 mutex。 创建和销毁筛选器工厂和筛选器都与此互斥体同步。 某些即插即用和电源管理操作也与此 mutex 同步。 微型驱动程序重点介绍了关于设备 mutex 的两个主要问题。

如果已持有设备互斥体，则 *只能* 将对象层次结构从设备缩小为单独的筛选器。 因此，在通过调用 [**KsCreateFilterFactory**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)手动创建筛选器工厂之前，微型驱动程序必须获取设备互斥体。 在遍历对象层次结构之前，微型驱动程序还必须通过调用 **Ks**_xxx_*_GetFirstChild_*_xxx_ 和 **ks**_xxx_*_GetNextSibling_*_xxx_ 函数来获取设备互斥体。

AVStream 在收到以下请求时代表微型驱动程序持有设备互斥体：

-   [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](../kernel/irp-mn-query-stop-device.md)

-   [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md)

-   [*PostStart 调度*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevice)

-   [**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)

-   [**IRP \_ MN \_ 查询 \_ 能力**](../kernel/irp-mn-query-power.md)

-   [**IRP \_ MN \_ 设置 \_ 电源**](../kernel/irp-mn-set-power.md)

-   对筛选器和 pin 的睡眠和唤醒通知。 请参阅 [**KsFilterRegisterPowerCallbacks**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterregisterpowercallbacks) 和 [**KsPinRegisterPowerCallbacks**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinregisterpowercallbacks)。

请务必注意，无法以递归方式获取设备互斥体。 请看下面的示例。 AVStream 收到休眠通知。 如上所述，它代表微型驱动程序使用设备互斥体。 然后，如果 AVStream 在线程 A 的上下文中调用微型驱动程序提供的回调例程，则微型驱动程序不能随后尝试获取线程 A 中的设备 mutex。这样做会使线程 A 自行发生死锁。

AVStream 通常会在已持有设备 mutex 时获取筛选器控件互斥体。 因此，通常情况下，已采用筛选器控件互斥体的线程不应随后获取设备互斥体。

若要操作设备 mutex，请使用以下函数：

[**KsAcquireDevice**](/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)、 [ **KsReleaseDevice**](/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)

 

