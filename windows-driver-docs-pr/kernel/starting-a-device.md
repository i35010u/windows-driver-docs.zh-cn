---
title: 启动设备
description: 启动设备
ms.assetid: c52588cf-04c8-420d-a68e-a8754a65d546
keywords:
- PnP WDK 内核，启动设备
- 即插即用 WDK 内核，启动设备
- 启动 PnP 设备
- DispatchPnP 例程
- IoCompletion 例程
- 未能启动 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332a15b203efc5e357474696ac2f37d963ead42f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836240"
---
# <a name="starting-a-device"></a>启动设备





PnP 管理器发送[**IRP\_MN\_开始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)向驱动程序\_设备请求，以启动新枚举的设备或重新启动已停止的、用于资源重新平衡的现有设备。

函数和筛选器驱动程序必须设置一个[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，传递**IRP\_MN\_** 在设备堆栈中\_设备请求，并推迟其启动操作，直到所有较低版本的驱动程序都已完成 IRP。 父总线驱动程序（设备堆栈中的底部驱动程序）必须是第一个要在设备上执行其启动操作的驱动程序，然后其他驱动程序才能访问设备。

若要确保启动操作的正确顺序，Windows 2000 和更高版本的 Windows 上的 PnP 管理器推迟公开设备接口，并阻止为设备创建请求，直到开始 IRP 成功。

如果设备的驱动程序失败， **IRP\_MN\_启动\_设备**请求，则 PnP 管理器会将[**IRP\_MN 发送到设备堆栈\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求（在 windows 2000 和更高版本的 windows 上）。 为响应此 IRP，设备的驱动程序将撤消其启动操作（如果已成功启动 IRP），撤消其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)操作，并脱离设备堆栈。 PnP 管理器将此类设备标记为 "启动失败"。

本部分包括以下主题：

[在函数驱动程序中启动设备](starting-a-device-in-a-function-driver.md)

[在筛选器驱动程序中启动设备](starting-a-device-in-a-filter-driver.md)

[在总线驱动程序中启动设备](starting-a-device-in-a-bus-driver.md)

[用于启动设备的设计指南](design-guidelines-for-starting-devices.md)

 

 




