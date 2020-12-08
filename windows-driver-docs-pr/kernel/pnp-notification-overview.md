---
title: PnP 通知概述
description: PnP 通知概述
keywords:
- PnP WDK 内核，通知
- 即插即用 WDK 内核，通知
- 通知 WDK PnP，关于通知
- 事件通知 WDK PnP
- EventCategoryDeviceInterfaceChange 通知
- EventCategoryTargetDeviceChange 通知
- EventCategoryHardwareProfileChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c7e7f589df5e198b0e2154f7c53d12ebd93d99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838441"
---
# <a name="pnp-notification-overview"></a>PnP 通知概述





PnP 管理器提供了一种机制，使驱动程序和应用程序在特定设备或系统上发生特定事件时获得通知。 驱动程序可以注册以下类别的事件的通知：

-   **EventCategoryDeviceInterfaceChange**

    当驱动程序在设备接口上注册此类事件时，PnP 管理器会通知驱动程序以下事件：

    <a href="" id="guid-device-interface-arrival"></a>GUID \_ 设备 \_ 接口 \_ 到达  
    指示已启用指定类的设备接口。 例如，用户已将新磁盘添加到计算机，卷管理器启用了新卷 (类 "卷" ) 的设备接口。

    <a href="" id="guid-device-interface-removal"></a>GUID \_ 设备 \_ 接口 \_ 删除  
    指示已禁用指定类的设备接口。

    有关设备接口的详细信息，请参阅 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 和相关的例程。

-   **EventCategoryTargetDeviceChange**

    当驱动程序在设备上注册此类事件时，PnP 管理器会在设备上发生以下事件时通知驱动程序：

    <a href="" id="guid-target-device-query-remove"></a>GUID \_ 目标 \_ 设备 \_ 查询 \_ 删除  
    指示 PnP 管理器即将删除设备的驱动程序。 若干操作可能导致此事件，包括：用户已请求从计算机中删除指定的设备，或者用户已发出设备的更新驱动程序请求。 此通知请求设备的驱动程序批准或拒绝即将执行的删除操作。

    <a href="" id="guid-target-device-remove-complete"></a>GUID \_ 目标 \_ 设备 \_ 删除 \_ 完成  
    指示指定的设备已从计算机中删除或用户正在更改设备的驱动程序 (s) 。

    <a href="" id="guid-target-device-remove-cancelled"></a>已 \_ 取消 GUID 目标 \_ 设备 \_ 删除 \_  
    指示已取消指定设备上即将删除的删除操作。

    <a href="" id="guid-xxx---custom-events-"></a>GUID \_ *XXX* (自定义事件)   
    指示在指定的设备上发生了自定义事件。

    驱动程序编写器可以为设备定义自定义事件。 当驱动程序 (或另一个相关组件) 通知 PnP 管理器自定义事件发生时，PnP 管理器将通知在设备上注册了目标设备更改通知的所有组件。

    与注册设备接口更改不同（可将其视为接口的 "被动"），注册目标设备更改表示设备上出现 "活动" 的兴趣。

-   **EventCategoryHardwareProfileChange**

    此类别包括以下事件：

    <a href="" id="guid-hwprofile-query-change"></a>GUID \_ HWPROFILE 中 \_ 查询 \_ 更改  
    指示用户已请求更改计算机的硬件配置文件。 PnP 管理器使用此通知来询问注册的组件是否可以更改硬件配置文件而不中断系统操作。 已注册的组件通常会成功执行这些查询请求。

    <a href="" id="guid-hwprofile-change-complete"></a>GUID \_ HWPROFILE 中 \_ 更改 \_ 完成  
    指示计算机的硬件配置文件已更改。 如果驱动程序维护配置文件特定的设置，则此类驱动程序应在硬件配置文件更改后刷新这些设置。

    <a href="" id="guid-hwprofile-change-cancelled"></a>GUID \_ HWPROFILE 中 \_ 更改已 \_ 取消  
    指示即将取消即将发生的硬件配置文件更改。

对于内核模式组件，PnP 通知的工作原理如下：

1.  驱动程序通过调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)来注册事件类别的通知。

    PnP 通知回调例程保持注册状态，直到驱动程序显式删除注册。

2.  当注册的类别中发生事件时，PnP 管理器会调用驱动程序的回调例程。

3.  驱动程序通过调用 [**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来删除回调注册。

驱动程序不能生成同步事件，也不能在处理关闭过程中等待异步事件发生。

有关 PnP 通知的详细信息，请参阅以下部分：

[有关编写 PnP 通知回调例程的指导原则](guidelines-for-writing-pnp-notification-callback-routines.md)

[使用 PnP 设备接口更改通知](using-pnp-device-interface-change-notification.md)

[使用 PnP 目标设备更改通知](using-pnp-target-device-change-notification.md)

[使用 PnP 硬件配置文件更改通知](using-pnp-hardware-profile-change-notification.md)

[使用 PnP 自定义通知](using-pnp-custom-notification.md)

 

