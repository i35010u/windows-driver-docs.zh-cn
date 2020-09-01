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
ms.openlocfilehash: f5ea6e740e61fe7c361987020c4bf8e882fff2f5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191839"
---
# <a name="registering-for-device-interface-change-notification"></a>注册设备接口更改通知





驱动程序通过调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)注册设备接口到达和删除事件的通知。

以下信息适用于为设备接口更改通知调用此例程：

-   指定**EventCategoryDeviceInterfaceChange**的*EventCategory* 。

-   *EventCategoryData* 必须指向设备接口类的 GUID。

    接口类的 GUID 通常在标头文件中定义，该标头文件包含接口的结构、常量等。

-   指定 *EventCategoryFlags* of PNPNOTIFY \_ DEVICE \_ INTERFACE INCLUDE an \_ \_ 现有 \_ interface。

    此标志指示 PnP 管理器注册 *CallbackRoutine* 以供指定类的未来设备接口到达和出发，并为已激活的任何相关设备接口立即调用 *CallbackRoutine* 。

    驱动程序可以调用 [**IoGetDeviceInterfaces**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来获取特定类的现有接口列表，然后在不使用此标志的情况下注册其回调例程，但使用标志会更容易，并可避免潜在的计时问题。

-   如果需要，请指定 PnP 管理器将传递到回调例程的驱动程序定义的 *上下文*。

为响应设备接口到达通知而打开设备的句柄的驱动程序应在设备上注册 **EventCategoryTargetDeviceChange** 事件。  (参阅 [使用 PnP 目标设备更改通知](using-pnp-target-device-change-notification.md)。 ) 

驱动程序通过使用**IoRegisterPlugPlayNotification**返回的*NotificationEntry*调用[**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来取消通知注册。

 

