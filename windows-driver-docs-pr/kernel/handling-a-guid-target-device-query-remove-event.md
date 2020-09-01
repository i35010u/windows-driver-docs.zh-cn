---
title: 处理 GUID_TARGET_DEVICE_QUERY_REMOVE 事件
description: 处理 GUID_TARGET_DEVICE_QUERY_REMOVE 事件
ms.assetid: f3e867c5-f7b8-40d2-a6cc-c5cb82e0b59b
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_QUERY_REMOVE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2b8a04363cf6dd8e1108e300f4bb130e9428c61
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183863"
---
# <a name="handling-a-guid_target_device_query_remove-event"></a>处理 GUID \_ 目标 \_ 设备 \_ 查询 \_ 删除事件





在 PnP 管理器发送 [**IRP \_ MN 查询 \_ 将 \_ \_ device**](./irp-mn-query-remove-device.md) IRP 发送到设备的驱动程序之前，它会调用为设备上的 **EventCategoryTargetDeviceChange** 注册的任何通知回调例程。 PnP 管理器指定*NotificationStructure*。**Event** GUID \_ 目标 \_ 设备 \_ 查询删除的事件 \_ 。

为响应此类通知，回调例程确定是否可以在不中断系统的情况下删除设备。

如果不应删除设备，则回调例程返回状态 "未 \_ 成功"。 在此状态下，PnP 管理器将中止查询删除处理，并且不会删除设备。

如果可以删除设备，则回调例程应执行任何适当的操作以准备设备删除，例如关闭设备上任何打开的句柄 (如有可能) 。 如果句柄在设备上保持打开状态，则 PnP 管理器无法删除设备，PnP 管理器会中止查询-删除处理。

成功处理 GUID \_ 目标 \_ 设备 \_ 查询 \_ 删除事件时，通知回调例程应：

-   关闭设备的所有打开的句柄。

-   如果驱动程序对文件对象具有未完成的引用，则取消引用文件对象。

-   保持注册以供将来 **EventCategoryTargetDeviceChange** 通知。 这一点很重要，因为可能会取消即将发生的删除操作。

关闭设备的句柄不会取消驱动程序注册到 PnP 目标设备更改通知。 PnP 管理器仍可调用驱动程序的通知回调例程，但在这种情况下， *NotificationStructure* 中的文件对象无效。

 

