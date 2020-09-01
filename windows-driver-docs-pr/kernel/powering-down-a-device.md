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
ms.openlocfilehash: f586229af83c99575c0705c88dbcbfc008a26021
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189320"
---
# <a name="powering-down-a-device"></a>关闭设备的电源





除非为设备启用了唤醒功能，否则其驱动程序会在系统关闭时为其提供支持。 删除或意外删除后，必须始终关闭设备电源。

删除设备后，即插即用管理器会将 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求发送到设备堆栈。 为了响应此 IRP，设备的驱动程序应确保设备已关闭。 关闭设备是删除处理的隐含部分;设备电源策略所有者不需要为**PowerDeviceD3**发送[**IRP \_ MN \_ SET \_ power**](./irp-mn-set-power.md) 。

当驱动程序处理 **IRP \_ MN \_ REMOVE \_ 设备** 请求时，它们会等待挂起的 i/o 完成，执行任何必要的删除处理，调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器设备处于状态 D3，并删除其为此设备创建的设备对象。 通常，总线驱动程序会关闭设备电源。

如果意外从 Windows 2000 或更高版本的操作系统中删除了某个设备，即插即用管理器会将 [**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) 请求发送到相应的设备堆栈的顶部。 为了响应此 IRP，设备的驱动程序应执行意外删除处理，如 [处理 IRP \_ MN \_ 意外 \_ 删除请求](handling-an-irp-mn-surprise-removal-request.md)中所述。

系统关闭时，电源管理器会将 **IRP \_ MN \_ 设置 \_ ** 为系统电源状态 (为 S4 或 S5) 。 当设备电源策略所有者接收到此 IRP 时，它应为**PowerDeviceD3**发送**irp \_ MN \_ SET \_ power** ，以便较低的驱动程序可以完成工作并关闭设备电源。

驱动程序可以选择对其设备执行空闲检测，也可以请求电源管理器执行空闲检测，以便在不使用设备时将其关闭。 有关详细信息，请参阅 [检测空闲设备](detecting-an-idle-device.md)。

 

