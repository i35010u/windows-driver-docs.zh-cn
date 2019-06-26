---
title: 关闭设备的电源
description: 关闭设备的电源
ms.assetid: d2525e15-9590-4fc0-955c-ca3540c13375
keywords:
- 设备电源列表 WDK 内核
- 下设备 WDK 内核增强
- IRP_MN_REMOVE_DEVICE
- 关闭设备 WDK 电源管理
- 自动电源列表 WDK 内核
- 关闭电源管理 WDK 内核
- 关闭 power WDK 内核
- Irp WDK 电源管理
- 意外删除 WDK 电源管理
- 设备删除 WDK 电源管理
- 删除设备
- I/O WDK 电源管理
- 意外的设备删除 WDK 电源管理
- 空闲检测 WDK 电源管理
- 节省电源 WDK 内核
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d45f2103467af7e2b0aa543b78b5f4873787e45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374185"
---
# <a name="powering-down-a-device"></a>关闭设备的电源





除非为唤醒启用了设备，其驱动程序它关闭电源系统关闭时。 始终必须在删除或意外删除时关闭设备。

移除某个设备，插管理器将发送[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)对设备堆栈请求。 在响应此 IRP，设备的驱动程序应确保设备接通电源关闭。 关闭该设备是隐式删除处理; 组成部分设备电源策略所有者不需要发送[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)对于**PowerDeviceD3**。

驱动程序处理**IRP\_MN\_删除\_设备**请求，请等待挂起的 I/O 完成，执行任何必要的删除处理时，调用[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)通知设备处于状态 D3，电源管理器并删除它们创建为此设备的设备对象。 通常情况下，总线驱动程序将关闭设备电源。

如果从 Windows 2000 或更高版本操作系统意外移除某个设备，插管理器发送[ **IRP\_MN\_惊讶\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)对堆栈顶部的相应设备的请求。 在此 IRP 响应，设备的驱动程序应执行意外删除处理，如中所述[处理 IRP\_MN\_惊讶\_删除请求](handling-an-irp-mn-surprise-removal-request.md)。

在系统关闭电源管理器将发送**IRP\_MN\_设置\_POWER**系统电源状态 （S4 或 S5）。 当设备电源策略所有者将会收到此 IRP 时，它应发送**IRP\_MN\_设置\_POWER**有关**PowerDeviceD3**以便较低的驱动程序来完成其工作和电源向下设备。

驱动程序可以选择执行空闲检测其设备，或者可以请求电源管理器执行空闲检测，以便可以在不使用下，在打开设备。 有关详细信息，请参阅[检测空闲的设备](detecting-an-idle-device.md)。

 

 




