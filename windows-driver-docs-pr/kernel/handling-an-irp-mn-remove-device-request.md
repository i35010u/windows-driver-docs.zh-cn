---
title: 处理 IRP_MN_REMOVE_DEVICE 请求
description: 处理 IRP_MN_REMOVE_DEVICE 请求
keywords:
- IRP_MN_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d3accf148b14912bc2f439b68d164e9ccb520e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801709"
---
# <a name="handling-an-irp_mn_remove_device-request"></a>处理 IRP \_ MN \_ 删除 \_ 设备请求





PnP 管理器使用此 IRP 来指示驱动程序删除设备的软件表示形式 (设备对象等) 。 当设备以有序的方式被删除时，PnP 管理器会发送此 IRP (例如，通过 "拔出或弹出硬件程序" 中的用户启动) ，会意外 (用户从其槽拉取设备，而无需事先警告) ，或当用户请求更新驱动程序时。

在 Windows 2000 和更高版本的系统上，当设备管理器禁用设备时，PnP 管理器会发送此 IRP。 在 Windows 98/Me 上，PnP 管理器改为发送停止 Irp。 有关详细信息，请参阅 [停止设备](stopping-a-device.md) 。

在将此 IRP 发送到设备的驱动程序之前，PnP 管理器会执行以下操作：

-   将 **IRP \_ MN \_ 删除 \_ 设备** 请求发送到设备的子节点（如果有）。

-   通知所有用户模式组件和内核模式驱动程序，这些驱动程序已注册为通知删除设备。 PnP 管理器会调用在设备的句柄上注册目标设备通知的任何用户模式组件，并调用任何为 **EventCategoryTargetDeviceChange** 注册的内核模式驱动程序。

-    (在 Windows 2000 和更高版本的系统上) 如果在设备上装入了文件系统，则 PnP 管理器会将删除请求发送到文件系统和任何文件系统筛选器。 作为响应，文件系统通常会卸除卷。

设备堆栈中的顶部驱动程序处理删除 IRP，并将其传递给下一个较低的驱动程序。 设备的父总线驱动程序是执行其删除设备操作的最后一个驱动程序。 驱动程序会在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理删除 irp。

在驱动程序为 **IRP \_ MN \_ 删除 \_ 设备** 请求成功返回成功之前，必须确保已释放设备的所有资源。 在卸载驱动程序之前，此 IRP 可以是最后一次调用。

删除一个设备可以创建删除一系列其他设备的需求。 PnP 管理器将其他设备对象从顶部向下移动到根设备级别。

本节介绍以下内容：

[在函数驱动程序中删除设备](removing-a-device-in-a-function-driver.md)

[在筛选器驱动程序中删除设备](removing-a-device-in-a-filter-driver.md)

[在总线驱动程序中删除设备](removing-a-device-in-a-bus-driver.md)

 

