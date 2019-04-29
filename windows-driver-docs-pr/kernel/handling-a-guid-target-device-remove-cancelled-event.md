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
ms.openlocfilehash: 04d6dfcb47f6ce0c590e78faee78958798087407
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359867"
---
# <a name="handling-a-guidtargetdeviceremovecancelled-event"></a>处理一个 GUID\_目标\_设备\_删除\_已取消事件





如果[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)请求失败，即插即用管理器将发送[ **IRP\_MN\_取消\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550823) IRP 到设备的驱动程序。 取消按钮删除 IRP 成功完成后，即插即用管理器会为注册的回调例程调用任何通知**EventCategoryTargetDeviceChange**在设备上。 PnP 管理器指定*NotificationStructure*。**事件**的 GUID\_目标\_设备\_删除\_已取消。

当处理一个 GUID\_目标\_设备\_删除\_已取消事件通知回调例程应：

-   目标设备通知，重新注册。

    因为该驱动程序关闭响应的查询删除通知中以前的注册句柄，该驱动程序必须打开新的句柄。 该驱动程序必须：

    1.  删除与旧的注册[ **IoUnregisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff550398)。

    2.  打开设备的新句柄。

    3.  使用新的句柄上的通知重新注册**IoRegisterPlugPlayNotification**。

 

 




