---
title: 处理设备电源策略所有者中的系统集 Power IRP
description: 处理设备电源策略所有者中的系统集 Power IRP
ms.assetid: f6206455-142b-4f3f-ae5a-d8e79386bce3
keywords:
- 设置 power Irp WDK 电源管理
- 设备电源策略所有者 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8e8cb45d24f56a788d75a8c91cca222847fae21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525792"
---
# <a name="handling-a-system-set-power-irp-in-a-device-power-policy-owner"></a>处理设备电源策略所有者中的系统集 Power IRP





以响应系统集 power IRP[电源策略所有者](managing-device-power-policy.md)设备堆栈负责使其设备堆栈的适当的设备电源状态。

作为通用规则，当设备电源策略所有者收到[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)系统电源状态，它应响应通过传递系统设备在堆栈的下层组 power IRP。 设备电源策略所有者还应响应通过发送设备堆栈的下层**IRP\_MN\_设置\_POWER**中的相应设备电源状态为[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 堆栈中的所有驱动程序已完成设备后集 power IRP 设备电源策略所有者完成系统集 power IRP。

但是，为了提高系统恢复性能，不具有子设备的设备的设备电源所有者应使用不同的方法来减少所需的系统返回到的时间[处于工作状态 S0](system-working-state-s0.md)从[睡眠状态](system-sleeping-states.md)。 在这种情况下，在对系统的响应中返回到工作状态 S0、 系统集 power IRP 设备电源策略所有者应执行以下一系列操作：

1.  收到后**IRP\_MN\_设置\_POWER** S0 系统电源状态中的驱动程序的 IRP [DispatchPower 例程](dispatchpower-routines.md)，将*IoCompletion* IRP 和传递在堆栈的下层 IRP 例程。

2.  在中*IoCompletion*在步骤 (1) 中的例程集请求**IRP\_MN\_设置\_POWER** IRP 为相应的设备电源状态，然后立即完成系统集 power IRP。 该驱动程序不应等待设备集电源 Irp 完成之前完成系统集 power IRP。 *IoCompletion*较低级别的所有驱动程序已完成系统后，将执行例程集 power IRP 和系统集 power IRP 传递回驱动程序的功能的设备对象 (FDO)。

3.  执行任何所需的特定于设备的初始化。

4.  完成设备设置 power IRP 发送在步骤 (2) 中。

5.  处理 I/O 请求时在设备处于排队[休眠状态的设备](device-sleeping-states.md)。

内核电源管理器具有一组有限的 IRP 调度队列，并且必须快速通知对系统工作状态 S0 返回系统中的所有设备。 无法完成系统的驱动程序集 power IRP 尽可能快地阻止其他设备获取其系统集 power IRP，可能会在系统电源状态转换期间，总体系统性能产生负面影响。

有关详细信息处理系统集 power Irp，看到以下信息：

[确定正确的设备电源状态](determining-the-correct-device-power-state.md)

[在响应系统集 Power IRP 发送设备集 Power IRP](sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp.md)

 

 




