---
title: 启动设备
description: 启动设备
keywords:
- PnP WDK 内核，启动设备
- 即插即用 WDK 内核，启动设备
- 启动 PnP 设备
- DispatchPnP 例程
- IoCompletion 例程
- 未能启动 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f81549fa7a9704d8f8f9ac0f579db8427ab9be31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834409"
---
# <a name="starting-a-device"></a>启动设备





PnP 管理器将 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求发送到驱动程序，以启动新枚举的设备或重新启动已停止的、用于资源重新平衡的现有设备。

函数和筛选器驱动程序必须设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，将 **IRP \_ MN \_ START \_ device** 请求按设备堆栈，并推迟其启动操作，直到所有较低版本的驱动程序都已完成 IRP。 父总线驱动程序（设备堆栈中的底部驱动程序）必须是第一个要在设备上执行其启动操作的驱动程序，然后其他驱动程序才能访问设备。

若要确保启动操作的正确顺序，Windows 2000 和更高版本的 Windows 上的 PnP 管理器推迟公开设备接口，并阻止为设备创建请求，直到开始 IRP 成功。

如果设备的驱动程序无法通过 **irp \_ MN \_ 启动 \_ 设备** 请求，则 PnP 管理器会在 windows 2000 和更高版本的 windows) 上向设备堆栈 (发送 [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。 对于此 IRP，如果设备的驱动程序成功启动 IRP) 、撤消其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 操作并从设备堆栈分离，则设备的驱动程序将撤消其启动操作 (。 PnP 管理器将此类设备标记为 "启动失败"。

本部分涵盖了以下主题：

[在函数驱动程序中启动设备](starting-a-device-in-a-function-driver.md)

[在筛选器驱动程序中启动设备](starting-a-device-in-a-filter-driver.md)

[在总线驱动程序中启动设备](starting-a-device-in-a-bus-driver.md)

[启动设备的设计指导原则](design-guidelines-for-starting-devices.md)

 

