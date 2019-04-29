---
title: PnP 通知概述
description: PnP 通知概述
ms.assetid: 134a1ea1-78c2-4bab-b5e9-ae21901772ea
keywords:
- 即插即用 WDK 内核通知
- 即插即用和播放 WDK 内核通知
- 通知即插即用，有关通知的 WDK
- 事件通知 WDK 即插即用
- EventCategoryDeviceInterfaceChange 通知
- EventCategoryTargetDeviceChange 通知
- EventCategoryHardwareProfileChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 643420c426f8dd9b439312306cdefbe1e7da3c32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369219"
---
# <a name="pnp-notification-overview"></a>PnP 通知概述





PnP 管理器提供了一种机制，用于驱动程序和应用程序在发生特定事件的特定设备上或在系统上通常时得到通知。 驱动程序可以注册以下类别的事件的通知：

-   **EventCategoryDeviceInterfaceChange**

    当驱动程序注册为此类别的设备接口上的事件时，即插即用管理器会通知驱动程序的以下事件：

    <a href="" id="guid-device-interface-arrival"></a>GUID\_DEVICE\_INTERFACE\_ARRIVAL  
    指示启用了指定的类的设备接口。 例如，将用户添加到计算机的新磁盘和卷管理器启用新卷 （类"卷"的设备接口）。

    <a href="" id="guid-device-interface-removal"></a>GUID\_DEVICE\_INTERFACE\_REMOVAL  
    指示已禁用了指定的类的设备接口。

    请参阅[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)和相关的例程的有关设备接口的详细信息。

-   **EventCategoryTargetDeviceChange**

    当驱动程序注册为此类别的设备上的事件时，即插即用管理器会在设备上发生以下事件时通知该驱动程序：

    <a href="" id="guid-target-device-query-remove"></a>GUID\_目标\_设备\_查询\_删除  
    指示要删除的设备驱动程序 PnP 管理器。 多个操作可能会导致此事件，包括： 用户已请求从计算机中删除指定的设备或用户发出的设备的更新驱动程序请求。 此通知请求要批准或否决即将发生的删除操作的设备的驱动程序。

    <a href="" id="guid-target-device-remove-complete"></a>GUID\_目标\_设备\_删除\_完成  
    指示指定的设备已从计算机中删除或用户正在更改设备驱动程序。

    <a href="" id="guid-target-device-remove-cancelled"></a>GUID\_目标\_设备\_删除\_已取消  
    指示指定的设备上的即将发生删除操作已取消。

    <a href="" id="guid-xxx---custom-events-"></a>GUID\_*XXX* （自定义事件）  
    指示指定的设备上已发生的自定义的事件。

    驱动程序编写器可以定义自定义事件的设备。 当驱动程序 （或另一个相关的组件） 通知的自定义事件已发生的即插即用管理器时，即插即用的管理器会通知为目标设备注册的任何组件更改设备上的通知。

    与注册的设备接口更改，可被视为在界面中的"被动"感兴趣，不同的目标设备更改注册指示设备中的"活动"关注。

-   **EventCategoryHardwareProfileChange**

    此类别包括以下事件：

    <a href="" id="guid-hwprofile-query-change"></a>GUID\_HWPROFILE\_查询\_更改  
    指示用户已请求更改计算机的硬件配置文件。 即插即用 manager 使用此通知来让已注册的组件是否可以更改硬件配置文件而不会中断系统操作。 已注册的组件通常会成功这些查询请求。

    <a href="" id="guid-hwprofile-change-complete"></a>GUID\_HWPROFILE\_更改\_完成  
    指示已更改的计算机的硬件配置文件。 如果驱动程序维护特定于配置文件的设置，这样的驱动程序应在硬件配置文件更改后刷新这些设置。

    <a href="" id="guid-hwprofile-change-cancelled"></a>GUID\_HWPROFILE\_更改\_已取消  
    指示即将进行的硬件配置文件更改已被取消。

即插即用通知，如下所示适用于内核模式组件：

1.  驱动程序通过调用注册的事件类别的通知[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。

    即插即用通知回调例程将保持已注册，直到该驱动程序显式删除的注册。

2.  PnP 管理器中的已注册的类别的事件发生时调用驱动程序的回调例程。

3.  该驱动程序通过调用来消除回调注册[ **IoUnregisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff550398)。

不，驱动程序必须生成同步事件，或者等待要关闭的处理过程中出现的异步事件。

即插即用通知的详细信息，请参阅以下各节：

[编写即插即用通知回调例程准则](guidelines-for-writing-pnp-notification-callback-routines.md)

[使用即插即用设备接口更改通知](using-pnp-device-interface-change-notification.md)

[使用即插即用的目标设备更改通知](using-pnp-target-device-change-notification.md)

[使用即插即用硬件配置文件更改通知](using-pnp-hardware-profile-change-notification.md)

[使用即插即用的自定义通知](using-pnp-custom-notification.md)

 

 




