---
title: 使用电源管理器例程进行空闲检测
description: 使用电源管理器例程进行空闲检测
ms.assetid: 6a89b2eb-d987-4722-b521-9df93153d957
keywords:
- 空闲检测 WDK 电源管理
- PoRegisterDeviceForIdleDetection
- PoSetDeviceBusy
- 电源管理器 WDK 内核
- 空闲超时 WDK 电源管理
- 超时 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac3295d9386489986d1b28e473797b755323aef2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381569"
---
# <a name="using-power-manager-routines-for-idle-detection"></a>使用电源管理器例程进行空闲检测





电源管理器支持通过空闲检测[ **PoRegisterDeviceForIdleDetection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterdeviceforidledetection)并[ **PoSetDeviceBusy** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程。

若要启用空闲检测其设备，设备电源策略所有者调用**PoRegisterDeviceForIdleDetection** ，并指定：

-   要应用时系统会针对性能进行优化的空闲超时值。

-   要应用时系统会针对节省进行优化的空闲超时值。

-   向其设备应转换在空闲时设备电源状态。

**PoRegisterDeviceForIdleDetection**将指针返回到空闲的计数器，该驱动程序使用更高版本来禁用空闲检测。 调用方**PoRegisterDeviceForIdleDetection**必须在 IRQL 运行&lt;调度\_级别。

驱动程序可以注册其设备的空闲检测后该设备已启动并且已准备好处理设备电源 Irp 的任何时间。 例如，驱动程序可能启用作为的一部分的空闲检测其*IoCompletion*常规的即插即用的启动设备 IRP。

任何给定设备的超时值应与设备的增益道具延迟成比例，并且根据观察到的设备的行为。 对于某些类型的设备，驱动程序可以指定节省和性能为-1 的设备类使用标准的电源策略超时的超时值。 请参阅详细信息的特定于设备的文档。

当设备正在使用中时，该驱动程序必须调用[ **PoSetDeviceBusy**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，并传递所返回的指针**PoRegisterDeviceForIdleDetection**。 **PoSetDeviceBusy**将重置空闲的计数器，从而重启设备空闲的倒计时。 该驱动程序应调用**PoSetDeviceBusy**在每次 I/O 操作。

若要确定设备是否处于空闲状态，电源管理器将使用当前系统电源策略 （节省或性能） 的驱动程序指定空闲超时值的空闲状态的计数器值进行比较。 请参阅 Microsoft Windows SDK for 与系统电源策略相关的函数。

当设备满足超时值时，一个设备的电源管理器发送集 power IRP，指定设备电源驱动程序对其调用中传递的状态**PoRegisterDeviceForIdleDetection**。 电源管理器不发送集 power IRP 之前发送 IRP 的查询。 堆栈中的驱动程序处理集 power IRP，因为它们会处理任何其他;它们必须及时地完成它并进行它们不能故障。 (请参阅[处理设备电源关闭 Irp](handling-device-power-down-irps.md)。)

该驱动程序不再需要空闲检测或不是准备好处理设备电源关闭 Irp，则应调用**PoRegisterDeviceForIdleDetection**再次，传递两个超时值为零。 设置为零的超时值禁用空闲检测 （电池） 节省和性能 (AC) 电源策略。 该驱动程序可以快速重新启用空闲检测;它只需调用**PoRegisterDeviceForIdleDetection**具有非零的超时值。 后驱动程序已注册设备，它可以启用和禁用空闲检测的更改超时值，即使设备已关机并重新唤醒。

 

 




