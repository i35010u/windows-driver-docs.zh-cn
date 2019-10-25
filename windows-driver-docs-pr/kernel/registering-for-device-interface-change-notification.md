---
title: 注册设备接口更改通知
description: 注册设备接口更改通知
ms.assetid: 680e4c5c-dac6-41b1-b754-aee782145ed0
keywords:
- 通知 WDK PnP，设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK PnP
- 正在注册设备接口更改通知
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f29e2a2487baf7649e5bd381aa6fefae2919d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827487"
---
# <a name="registering-for-device-interface-change-notification"></a>注册设备接口更改通知





驱动程序通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)注册设备接口到达和删除事件的通知。

以下信息适用于为设备接口更改通知调用此例程：

-   指定**EventCategoryDeviceInterfaceChange**的*EventCategory* 。

-   *EventCategoryData*必须指向设备接口类的 GUID。

    接口类的 GUID 通常在标头文件中定义，该标头文件包含接口的结构、常量等。

-   指定*EventCategoryFlags*的 PNPNOTIFY\_设备\_接口\_包括\_现有\_接口。

    此标志指示 PnP 管理器注册*CallbackRoutine*以供指定类的未来设备接口到达和出发，并立即调用*CallbackRoutine*的任何相关设备接口正在.

    驱动程序可以调用[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)来获取特定类的现有接口列表，然后在不使用此标志的情况下注册其回调例程，但使用标志会更容易，并可避免潜在的计时问题。

-   如果需要，请指定 PnP 管理器将传递到回调例程的驱动程序定义的*上下文*。

为响应设备接口到达通知而打开设备的句柄的驱动程序应在设备上注册**EventCategoryTargetDeviceChange**事件。 （请参阅[使用 PnP 目标设备更改通知](using-pnp-target-device-change-notification.md)。）

驱动程序通过使用**IoRegisterPlugPlayNotification**返回的*NotificationEntry*调用[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来取消通知注册。

 

 




