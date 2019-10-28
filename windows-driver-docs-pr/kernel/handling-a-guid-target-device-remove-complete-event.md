---
title: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
description: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
ms.assetid: 7f20faae-b5ef-4a64-9150-bff14b04aaa4
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_COMPLETE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26677ce4388df92ca279679c871eec0d51db16ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838676"
---
# <a name="handling-a-guid_target_device_remove_complete-event"></a>处理 GUID\_目标\_设备\_删除\_完成事件





在 PnP 管理器发送[**IRP\_MN 之前\_将\_设备 IRP 删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)到设备的驱动程序上，PnP 管理器将调用为**EventCategoryTargetDeviceChange**注册的任何内核模式通知回调例程设备。 PnP 管理器指定*NotificationStructure*。GUID\_目标\_设备的**事件**\_删除\_完成。

当处理 GUID\_目标\_设备\_删除\_完成事件时，通知回调例程应：

-   删除设备上的通知注册。

    设备已被删除，因此驱动程序调用[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来删除通知注册。

    设备仍可能在物理上出现在计算机上，但已删除所有设备对象，但设备不可用。

-   如果驱动程序没有收到上一个查询-删除通知，请执行意外删除处理。

    如果设备被意外删除，则 PnP 管理器会向注册的驱动程序发送删除完成通知，而无需之前的查询-删除通知。 在这种情况下，驱动程序必须执行任何必要的清理，例如关闭设备的任何句柄，并删除对文件对象的任何未完成的引用。

 

 




