---
title: 使用 PnP 自定义通知
description: 使用 PnP 自定义通知
ms.assetid: de5562f8-07a8-4f4e-ac49-58c789bd9fde
keywords:
- 通知 WDK PnP，自定义
- 自定义通知 WDK PnP
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 282612bb0b101b50e8ecb4a85f773d6be65a7880
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838342"
---
# <a name="using-pnp-custom-notification"></a>使用 PnP 自定义通知





驱动程序可以使用目标设备更改通知机制在设备上通知自定义事件。

定义自定义事件的程序员必须执行以下操作：

1.  为自定义事件定义新的 GUID。

    用**uuidgen.exe**或**guidgen.exe**生成 GUID （包含在 Microsoft Windows SDK 中）。 将 GUID 发布到适当的标头文件和文档中。

2.  编写代码来触发自定义事件。

    在内核模式下，驱动程序使用自定义 GUID 和设备的 PDO 调用[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange) 。 自定义事件只能从内核模式触发。

驱动程序编写器使用自定义通知和如下过程：

1.  驱动程序（或应用程序）注册自定义事件的通知。

    在内核模式下，驱动程序调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)并注册设备上的**EventCategoryTargetDeviceChange** 。

    在用户模式下，应用程序使用**RegisterDeviceNotification**注册。 有关详细信息，请参阅 Windows SDK。

2.  内核模式组件触发自定义事件。

3.  PnP 管理器调用设备上注册的通知例程。

    PnP 管理器调用已注册的用户模式回调例程，然后调用内核模式回调例程。

4.  用户模式通知完成时，内核模式驱动程序通知回调例程会响应自定义事件。

    有关通知回调例程的一般准则，请参阅[编写 PnP 通知回调例程的准则](guidelines-for-writing-pnp-notification-callback-routines.md)。 除了这些准则以外，自定义通知回调例程还不得从回调例程线程内打开设备的句柄。

 

 




