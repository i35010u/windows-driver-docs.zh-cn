---
title: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
description: 处理 GUID_TARGET_DEVICE_REMOVE_COMPLETE 事件
ms.assetid: 7f20faae-b5ef-4a64-9150-bff14b04aaa4
keywords:
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_COMPLETE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66256d99e32d2de03c1cb49147aa77fd323257d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385245"
---
# <a name="handling-a-guidtargetdeviceremovecomplete-event"></a>处理一个 GUID\_目标\_设备\_删除\_完成事件





PnP 管理器发送之前[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) IRP 到设备的驱动程序，即插即用管理器中调用任何内核模式通知回调为注册的例程**EventCategoryTargetDeviceChange**在设备上。 PnP 管理器指定*NotificationStructure*。**事件**的 GUID\_目标\_设备\_删除\_完成。

当处理一个 GUID\_目标\_设备\_删除\_完成事件通知回调例程应：

-   删除设备上的注册通知。

    设备已被删除，这样该驱动程序可以调用[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)以删除通知注册。

    设备可能仍会以物理方式出现在计算机上，但已删除设备的所有对象和该设备不是可供使用。

-   执行意外删除处理，如果该驱动程序未收到前一次的查询删除通知。

    如果意外删除的设备，即插即用管理器发送已注册的驱动程序而无需以前的查询删除通知删除完成通知。 在这种情况下，驱动程序包含执行任何必要的清理，如关闭任何到设备的句柄和删除任何未完成的引用文件对象。

 

 




