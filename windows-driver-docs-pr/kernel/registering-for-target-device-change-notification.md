---
title: 注册目标设备更改通知
description: 注册目标设备更改通知
ms.assetid: 5f7a9c44-c9a4-4ff8-a97d-ad2462b86af0
keywords:
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
- 注册目标设备更改通知
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f50583b3b101d28c2fa8b71e185efa0c30245b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373456"
---
# <a name="registering-for-target-device-change-notification"></a>注册目标设备更改通知

驱动程序通过调用注册的即插即用的目标设备更改事件通知[ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)。

以下信息适用于目标设备更改通知才能调用该例程：

-   指定*EventCategory*的**EventCategoryTargetDeviceChange**。

-   *EventCategoryData*必须指向请求通知时该设备的文件对象。

    如果驱动程序的回调例程需要访问的文件对象，该驱动程序应该采取出对之前调用该文件对象的引用**IoRegisterPlugPlayNotification**。

    如果驱动程序的回调例程不需要对文件对象的访问，所以该驱动程序不需要来引用对象。

    关闭文件对象之后，驱动程序将继续接收通知的设备，直到该驱动程序将删除其注册通知。 此设计允许驱动程序以接收通知的 GUID\_目标\_设备\_删除\_取消事件，例如。

-   指定驱动程序定义*上下文*PnP 管理器将传递给回调例程。

    驱动程序可能会使用*上下文*参数，以维护文件对象的当前状态有关的信息 （例如，它已关闭/删除）。

    驱动程序还可以使用*上下文*来存储它用于最初打开设备的路径。 驱动程序可以使用此路径以已取消删除操作后，重新打开该设备。 (请参阅[处理 GUID\_目标\_设备\_删除\_取消事件](handling-a-guid-target-device-remove-cancelled-event.md)有关详细信息。)

驱动程序通过调用来消除通知注册[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)与*NotificationEntry*返回的**IoRegisterPlugPlayNotification**。 如果驱动程序执行扩展上的文件对象的引用的注册用于通知和引用是仍未完成时，该驱动程序必须释放该引用后删除的注册。

 

 




