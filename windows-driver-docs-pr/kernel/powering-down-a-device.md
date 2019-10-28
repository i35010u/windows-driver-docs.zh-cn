---
title: 关闭设备的电源
description: 关闭设备的电源
ms.assetid: d2525e15-9590-4fc0-955c-ca3540c13375
keywords:
- 设备电源关闭 WDK 内核
- 关闭设备的设备 WDK 内核
- IRP_MN_REMOVE_DEVICE
- 关闭设备 WDK 电源管理
- 自动电源关闭 WDK 内核
- 关闭电源管理 WDK 内核
- 关闭 power WDK 内核
- Irp WDK 电源管理
- 意外删除 WDK 电源管理
- 设备删除 WDK 电源管理
- 删除设备
- I/o WDK 电源管理
- 意外的设备删除 WDK 电源管理
- 空闲检测 WDK 电源管理
- 保存电源 WDK 内核
- I/o 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b8fb0eb5ec4ce7e4db0c2e8d619e0fdea022077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838499"
---
# <a name="powering-down-a-device"></a>关闭设备的电源





除非为设备启用了唤醒功能，否则其驱动程序会在系统关闭时为其提供支持。 删除或意外删除后，必须始终关闭设备电源。

删除设备后，即插即用管理器会发送[**IRP\_MN\_删除设备堆栈\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求。 为了响应此 IRP，设备的驱动程序应确保设备已关闭。 关闭设备是删除处理的隐含部分;设备电源策略所有者不需要发送[**IRP\_MN\_集\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) for **PowerDeviceD3**。

当驱动程序处理**IRP\_MN\_删除\_设备**请求时，它们会等待挂起的 i/o 完成，执行任何必要的删除处理，并调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)来通知电源管理器设备处于状态 D3，并删除为此设备创建的设备对象。 通常，总线驱动程序会关闭设备电源。

如果意外地从 Windows 2000 或更高版本的操作系统中删除了某个设备，即插即用管理器会将[**IRP\_MN\_\_意外删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)请求发送到相应的设备堆栈的顶部。 为了响应此 IRP，设备的驱动程序应执行意外删除处理，如[处理 IRP\_MN\_意外\_删除请求](handling-an-irp-mn-surprise-removal-request.md)中所述。

系统关闭时，电源管理器会发送**IRP\_MN\_** 为系统电源状态（S4 或 S5）\_电源。 当设备电源策略所有者接收到此 IRP 时，它应发送**irp\_MN\_为 POWERDEVICED3 设置\_电源**，以便较低的驱动程序可以完成工作并关闭设备电源。

驱动程序可以选择对其设备执行空闲检测，也可以请求电源管理器执行空闲检测，以便在不使用设备时将其关闭。 有关详细信息，请参阅[检测空闲设备](detecting-an-idle-device.md)。

 

 




