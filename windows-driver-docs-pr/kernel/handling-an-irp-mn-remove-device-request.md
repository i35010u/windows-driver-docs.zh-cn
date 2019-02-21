---
title: 处理一个 IRP_MN_REMOVE_DEVICE 请求
description: 处理一个 IRP_MN_REMOVE_DEVICE 请求
ms.assetid: 1e0c8b41-5375-41dd-80eb-e48c0f513e01
keywords:
- IRP_MN_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ce4f40df7c67f63add6af8b88b7ef11b15c02f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543718"
---
# <a name="handling-an-irpmnremovedevice-request"></a>处理 IRP\_MN\_删除\_设备请求





PnP 管理器使用此 IRP 将驱动程序，以删除设备的软件表示形式 （设备对象等）。 PnP 管理器将发送此 IRP 惊讶 （用户从其槽而不发出警告之前从该设备），已以有序的方式 （例如，在程序中拔出或弹出硬件用户启动的），而删除了设备或用户请求来更新 drivers。

在 Windows 2000 和更高版本的系统，即插即用管理器将发送此 IRP 时设备管理器禁用的设备。 在 Windows 98 上 / PnP 管理器发送的而是停止 Irp。 请参阅[停止设备](stopping-a-device.md)有关详细信息。

PnP 管理器执行以下操作之前将此 IRP 发送到设备的驱动程序：

-   将发送**IRP\_MN\_删除\_设备**请求到设备的子项，如果有的话。

-   任何用户模式组件和内核模式驱动程序注册通知正在删除该设备的通知。 PnP 管理器的句柄在设备上的目标设备通知调用任何已注册的用户模式组件，并调用注册的任何内核模式驱动程序**EventCategoryTargetDeviceChange**。

-   （在 Windows 2000 和更高版本系统）如果在设备上装载文件系统后，即插即用管理器将删除请求发送到文件系统和任何文件系统筛选器。 在响应中，文件系统通常卸除卷。

设备堆栈中的顶部驱动程序处理删除 IRP，并将其传递给下一个较低的驱动程序。 设备的父总线驱动程序是最后一个驱动程序来执行其移除设备操作。 驱动程序句柄删除 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

驱动程序返回成功之前**IRP\_MN\_删除\_设备**请求，必须确保设备的所有资源都已都释放。 该驱动程序在卸载之前，此 IRP 可能是最后一次调用。

删除一个设备可以创建一系列的其他设备中删除的需求。 PnP 管理器协调到根设备级别最高级别中的其他设备对象的删除。

本部分介绍：

[在功能驱动程序中删除设备](removing-a-device-in-a-function-driver.md)

[在筛选器驱动程序中删除设备](removing-a-device-in-a-filter-driver.md)

[总线驱动程序中删除设备](removing-a-device-in-a-bus-driver.md)

 

 




