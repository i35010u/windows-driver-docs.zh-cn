---
title: 处理 GUID_TARGET_DEVICE_REMOVE_CANCELLED 事件
description: 处理 GUID_TARGET_DEVICE_REMOVE_CANCELLED 事件
ms.assetid: 19fe012b-3ed0-4356-999b-79b1d08dfbd6
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de151d5a610f2b01188b258671b3205b56907799
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183861"
---
# <a name="handling-a-guid_target_device_remove_cancelled-event"></a>处理 GUID \_ 目标 \_ 设备删除 \_ 已 \_ 取消事件





如果 [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](./irp-mn-query-remove-device.md) 请求失败，则 PnP 管理器会将 [**IRP \_ MN \_ \_ 删除 \_ 设备**](./irp-mn-cancel-remove-device.md) irp 发送到设备的驱动程序。 取消删除 IRP 成功完成后，PnP 管理器将调用为设备上的 **EventCategoryTargetDeviceChange** 注册的任何通知回调例程。 PnP 管理器指定*NotificationStructure*。**Event**已取消 GUID \_ 目标 \_ 设备 \_ 删除的事件 \_ 。

当处理 GUID \_ 目标 \_ 设备删除 \_ 已 \_ 取消事件时，通知回调例程应：

-   注册目标设备通知。

    由于驱动程序在响应查询-删除通知时关闭了上一个注册句柄，因此驱动程序必须打开一个新的句柄。 驱动程序必须：

    1.  删除旧注册和 [**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)。

    2.  为设备打开一个新的句柄。

    3.  通过 **IoRegisterPlugPlayNotification**重新注册新句柄上的通知。

 

