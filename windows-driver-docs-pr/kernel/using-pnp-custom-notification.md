---
title: 使用 PnP 自定义通知
description: 使用 PnP 自定义通知
ms.assetid: de5562f8-07a8-4f4e-ac49-58c789bd9fde
keywords:
- WDK 即插即用的自定义通知
- WDK 即插即用的自定义通知
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44ae6795262b4600251fa2e78dae896385a85404
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354219"
---
# <a name="using-pnp-custom-notification"></a>使用 PnP 自定义通知





驱动程序可以使用目标设备更改通知机制的设备上的自定义事件通知。

定义自定义事件程序员必须执行以下操作：

1.  定义自定义事件的新 GUID。

    生成的 GUID **Uuidgen**或**Guidgen** （中包括哪些 Microsoft Windows SDK）。 发布相应的头文件和文档中的 GUID。

2.  编写代码，以触发自定义事件。

    在内核模式驱动程序将调用[ **IoReportTargetDeviceChange** ](https://msdn.microsoft.com/library/windows/hardware/ff549625)与自定义的 GUID 和设备 PDO 的指针。 从内核模式下，才会触发自定义事件。

驱动程序编写器使用自定义通知使用的过程如下所示：

1.  驱动程序 （或应用程序） 注册的自定义事件的通知。

    在内核模式驱动程序将调用[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526) ，并注册**EventCategoryTargetDeviceChange**在设备上。

    在用户模式下，应用程序注册使用**RegisterDeviceNotification**。 请参阅 Windows SDK 的详细信息。

2.  内核模式组件触发自定义事件。

3.  PnP 管理器会调用在设备上注册的通知例程。

    PnP 管理器调用回调例程的已注册的用户模式，，然后调用内核模式回调例程。

4.  用户模式通知完成后，内核模式驱动程序通知回调 routine(s) 响应自定义事件。

    请参阅[准则编写即插即用通知回调例程](guidelines-for-writing-pnp-notification-callback-routines.md)有关通知回调例程的常规指导。 除了这些指导原则，自定义通知回调例程必须打开的句柄从回调例程线程内的设备。

 

 




