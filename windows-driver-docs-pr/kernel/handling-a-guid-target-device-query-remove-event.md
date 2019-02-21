---
title: 处理 GUID_TARGET_DEVICE_QUERY_REMOVE 事件
description: 处理 GUID_TARGET_DEVICE_QUERY_REMOVE 事件
ms.assetid: f3e867c5-f7b8-40d2-a6cc-c5cb82e0b59b
keywords:
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_QUERY_REMOVE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f72e34a78a1aae2ca450e8a4fc96d902afba6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554430"
---
# <a name="handling-a-guidtargetdevicequeryremove-event"></a>处理一个 GUID\_目标\_设备\_查询\_删除事件





PnP 管理器发送之前[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705) IRP 到设备的驱动程序，它会调用任何通知回调为注册的例程**EventCategoryTargetDeviceChange**在设备上。 PnP 管理器指定*NotificationStructure*。**事件**的 GUID\_目标\_设备\_查询\_删除。

在响应此类通知，回调例程确定是否可以无需中断在系统中删除该设备。

如果不应删除该设备，回调例程将返回状态\_未成功。 此状态响应，即插即用管理器中止查询删除处理并将不会删除设备。

如果可以删除该设备，回调例程应执行任何适当的操作，准备用于设备删除，如关闭任何句柄会打开在设备 （如果可能）。 如果句柄保留在设备上打开的即插即用管理器无法删除该设备，和 PnP 管理器中止查询删除处理。

已成功处理 GUID 时\_目标\_设备\_查询\_删除事件通知回调例程应：

-   关闭任何打开的句柄到设备。

-   如果驱动程序具有对该文件对象的未完成的引用，取消引用的文件对象。

-   保持已注册的未来**EventCategoryTargetDeviceChange**通知。 这非常重要，因为即将发生的删除操作，可能会取消。

关闭到设备的句柄不会取消的即插即用的目标设备更改通知的驱动程序的注册。 PnP 管理器仍然可以调用驱动程序的通知回调例程，但在此类调用中的文件对象*NotificationStructure*无效。

 

 




