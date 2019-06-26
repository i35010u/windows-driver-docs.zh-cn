---
title: 处理 GUID_TARGET_DEVICE_REMOVE_CANCELLED 事件
description: 处理 GUID_TARGET_DEVICE_REMOVE_CANCELLED 事件
ms.assetid: 19fe012b-3ed0-4356-999b-79b1d08dfbd6
keywords:
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3c8adea938b74a4c7f9eddfcfacf85c0f198dff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385252"
---
# <a name="handling-a-guidtargetdeviceremovecancelled-event"></a>处理一个 GUID\_目标\_设备\_删除\_已取消事件





如果[ **IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求失败，即插即用管理器将发送[ **IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device) IRP 到设备的驱动程序。 取消按钮删除 IRP 成功完成后，即插即用管理器会为注册的回调例程调用任何通知**EventCategoryTargetDeviceChange**在设备上。 PnP 管理器指定*NotificationStructure*。**事件**的 GUID\_目标\_设备\_删除\_已取消。

当处理一个 GUID\_目标\_设备\_删除\_已取消事件通知回调例程应：

-   目标设备通知，重新注册。

    因为该驱动程序关闭响应的查询删除通知中以前的注册句柄，该驱动程序必须打开新的句柄。 该驱动程序必须：

    1.  删除与旧的注册[ **IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)。

    2.  打开设备的新句柄。

    3.  使用新的句柄上的通知重新注册**IoRegisterPlugPlayNotification**。

 

 




