---
title: 注册目标设备更改通知
description: 注册目标设备更改通知
ms.assetid: 5f7a9c44-c9a4-4ff8-a97d-ad2462b86af0
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
- 正在注册目标设备更改通知
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7490335a9b315ad9d3c28b286c7a1c0d2c1b73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827463"
---
# <a name="registering-for-target-device-change-notification"></a>注册目标设备更改通知

驱动程序通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)来注册 PnP 目标设备更改事件的通知。

以下信息适用于针对目标设备更改通知调用此例程：

-   指定**EventCategoryTargetDeviceChange**的*EventCategory* 。

-   *EventCategoryData*必须指向请求通知的设备的文件对象。

    如果驱动程序的回调例程需要访问文件对象，则在调用**IoRegisterPlugPlayNotification**之前，驱动程序应在文件对象上执行引用。

    如果驱动程序的回调例程不需要访问文件对象，则驱动程序无需引用对象。

    文件对象关闭之后，驱动程序将继续接收设备的通知，直到驱动程序删除其通知注册。 此设计允许驱动程序接收 GUID\_目标\_设备的通知，\_删除\_取消的事件，例如。

-   指定 PnP 管理器将传递到回调例程的驱动程序定义的*上下文*。

    驱动程序可以使用*上下文*参数来维护有关文件对象的当前状态的信息（例如，已关闭/删除）。

    驱动程序还可以使用*上下文*来存储它最初打开设备所用的路径。 驱动程序可以在取消删除操作后使用此路径重新打开设备。 （有关详细信息，请参阅[处理 GUID\_目标\_设备\_删除\_取消事件](handling-a-guid-target-device-remove-cancelled-event.md)。）

驱动程序通过使用**IoRegisterPlugPlayNotification**返回的*NotificationEntry*调用[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来删除通知注册。 如果驱动程序在注册通知时已对文件对象进行了引用，但该引用仍未完成，则驱动程序必须在删除注册后释放该引用。

 

 




