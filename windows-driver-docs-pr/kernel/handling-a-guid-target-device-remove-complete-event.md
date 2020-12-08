---
title: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
description: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_COMPLETE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627a12dc2b183f50bc858491da580b14d7f06118
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792751"
---
# <a name="handling-a-guid_target_device_remove_complete-event"></a>处理 GUID \_ 目标 \_ 设备 \_ 删除 \_ 完成事件





在 PnP 管理器将 [**irp \_ MN \_ REMOVE \_ device**](./irp-mn-remove-device.md) IRP 发送到设备的驱动程序之前，pnp 管理器会调用为设备上的 **EventCategoryTargetDeviceChange** 注册的任何内核模式通知回调例程。 PnP 管理器指定 *NotificationStructure*。**Event** GUID \_ 目标 \_ 设备 \_ 删除完成的事件 \_ 。

当处理 GUID \_ 目标 \_ 设备 \_ 删除 \_ 完成事件时，通知回调例程应：

-   删除设备上的通知注册。

    设备已被删除，因此驱动程序调用 [**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification) 来删除通知注册。

    设备仍可能在物理上出现在计算机上，但已删除所有设备对象，但设备不可用。

-   如果驱动程序没有收到上一个查询-删除通知，请执行意外删除处理。

    如果设备被意外删除，则 PnP 管理器会向注册的驱动程序发送删除完成通知，而无需之前的查询-删除通知。 在这种情况下，驱动程序必须执行任何必要的清理，例如关闭设备的任何句柄，并删除对文件对象的任何未完成的引用。

 

