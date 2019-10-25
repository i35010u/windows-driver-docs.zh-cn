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
ms.openlocfilehash: cd7c54ded519fcecbff386e5d22539d2ad267a69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836668"
---
# <a name="handling-a-guid_target_device_remove_cancelled-event"></a>处理 GUID\_目标\_设备\_删除\_取消的事件





如果[**IRP\_MN\_QUERY\_"删除"\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求失败，则 PnP 管理器会将 IRP\_MN 发送到 "取消"\_"取消"\_[**删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)的驱动程序。 取消删除 IRP 成功完成后，PnP 管理器将调用为设备上的**EventCategoryTargetDeviceChange**注册的任何通知回调例程。 PnP 管理器指定*NotificationStructure*。GUID\_目标\_设备的**事件**\_删除\_取消。

当处理 GUID\_目标\_设备\_删除\_取消事件时，通知回调例程应：

-   注册目标设备通知。

    由于驱动程序在响应查询-删除通知时关闭了上一个注册句柄，因此驱动程序必须打开一个新的句柄。 驱动程序必须：

    1.  删除旧注册和[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)。

    2.  为设备打开一个新的句柄。

    3.  通过**IoRegisterPlugPlayNotification**重新注册新句柄上的通知。

 

 




