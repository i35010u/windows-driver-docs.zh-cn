---
title: 注册设备接口更改通知
description: 注册设备接口更改通知
ms.assetid: 680e4c5c-dac6-41b1-b754-aee782145ed0
keywords:
- 通知 WDK 即插即用设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK 即插即用
- 注册设备接口更改通知
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f1633ee6fae1e21fe51460221ba1c2bc1ab1df5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373460"
---
# <a name="registering-for-device-interface-change-notification"></a>注册设备接口更改通知





驱动程序通过调用注册的设备接口到达和删除事件通知[ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)。

以下信息适用于设备接口更改通知才能调用该例程：

-   指定*EventCategory*的**EventCategoryDeviceInterfaceChange**。

-   *EventCategoryData*必须指向设备接口类的 GUID。

    接口类的 GUID 通常定义为结构、 常量，依此类推，接口的头文件中。

-   指定*EventCategoryFlags*的 PNPNOTIFY\_设备\_接口\_INCLUDE\_现有\_接口。

    此标志指示要注册的即插即用管理器*CallbackRoutine*的未来设备接口到达和离开的指定类并调用*CallbackRoutine*立即为任何已处于活动状态的相关设备接口。

    驱动程序可以调用[ **IoGetDeviceInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces)若要获取特定类的现有接口的列表，然后注册其回调例程，而无需此标志，但使用标志是既简单又可避免潜在的计时问题。

-   指定驱动程序定义*上下文*，如果合适，即插即用管理器将传递给回调例程。

在对设备接口到达通知响应中打开的句柄设备的驱动程序应注册**EventCategoryTargetDeviceChange**在设备上的事件。 (请参阅[使用即插即用的目标设备更改通知](using-pnp-target-device-change-notification.md)。)

驱动程序通过调用取消通知注册[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)与*NotificationEntry*返回的**IoRegisterPlugPlayNotification**。

 

 




