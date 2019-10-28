---
title: 处理 IRP_MN_REMOVE_DEVICE 请求
description: 处理 IRP_MN_REMOVE_DEVICE 请求
ms.assetid: 1e0c8b41-5375-41dd-80eb-e48c0f513e01
keywords:
- IRP_MN_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff04f4fec994c2c96e8911051c6a1da8748a1a16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838662"
---
# <a name="handling-an-irp_mn_remove_device-request"></a>处理 IRP\_MN\_删除\_设备请求





PnP 管理器使用此 IRP 定向驱动程序以删除设备的软件表示形式（设备对象等）。 当设备以有序的方式（例如，由拔出或弹出硬件程序中的用户启动）出现意外的情况时，PnP 管理器会发送此 IRP （例如，用户在没有前一条警告的情况下从其槽拉取设备），或当用户请求更新 dri 时vers.

在 Windows 2000 和更高版本的系统上，当设备管理器禁用设备时，PnP 管理器会发送此 IRP。 在 Windows 98/Me 上，PnP 管理器改为发送停止 Irp。 有关详细信息，请参阅[停止设备](stopping-a-device.md)。

在将此 IRP 发送到设备的驱动程序之前，PnP 管理器会执行以下操作：

-   发送**IRP\_MN\_删除**设备子请求\_设备请求（如果有）。

-   通知所有用户模式组件和内核模式驱动程序，这些驱动程序已注册为通知删除设备。 PnP 管理器会调用在设备的句柄上注册目标设备通知的任何用户模式组件，并调用任何为**EventCategoryTargetDeviceChange**注册的内核模式驱动程序。

-   （在 Windows 2000 和更高版本的系统上）如果文件系统已装载到设备上，则 PnP 管理器会将删除请求发送到文件系统和任何文件系统筛选器。 作为响应，文件系统通常会卸除卷。

设备堆栈中的顶部驱动程序处理删除 IRP，并将其传递给下一个较低的驱动程序。 设备的父总线驱动程序是执行其删除设备操作的最后一个驱动程序。 驱动程序会在其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理删除 irp。

在驱动程序为 IRP 返回 success **\_MN\_删除\_设备**请求之前，必须确保已释放设备的所有资源。 在卸载驱动程序之前，此 IRP 可以是最后一次调用。

删除一个设备可以创建删除一系列其他设备的需求。 PnP 管理器将其他设备对象从顶部向下移动到根设备级别。

本部分介绍：

[在函数驱动程序中删除设备](removing-a-device-in-a-function-driver.md)

[删除筛选器驱动程序中的设备](removing-a-device-in-a-filter-driver.md)

[在总线驱动程序中删除设备](removing-a-device-in-a-bus-driver.md)

 

 




