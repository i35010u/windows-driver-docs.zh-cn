---
title: 处理设备电源策略所有者中的系统 Set-Power IRP
description: 处理设备电源策略所有者中的系统 Set-Power IRP
ms.assetid: f6206455-142b-4f3f-ae5a-d8e79386bce3
keywords:
- 设置电源 Irp WDK 电源管理
- 设备电源策略所有者 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e4b494d1b76137e1f8cbb5202dcd87b022f3916
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188971"
---
# <a name="handling-a-system-set-power-irp-in-a-device-power-policy-owner"></a>处理设备电源策略所有者中的系统 Set-Power IRP





为了响应系统设置-电源 IRP，设备堆栈的 [电源策略所有者](managing-device-power-policy.md) 负责将其设备堆栈置于适当的设备电源状态。

通常，当设备电源策略所有者接收到系统电源状态的 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 时，它应通过将系统设置-电源 IRP 向下传递到设备堆栈来做出响应。 设备电源策略所有者还应通过向下发送设备 stack IRP MN 为[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中的相应设备电源状态** \_ \_ 设置 \_ 电源**来做出响应。 堆栈中的所有驱动程序都完成设备设置-电源 IRP 后，设备电源策略所有者完成系统设置-power IRP。

但是，为了提高系统恢复性能，没有子设备的设备的设备电源所有者应使用不同的方法来减少系统从[睡眠状态](system-sleeping-states.md)返回到[工作状态 S0](system-working-state-s0.md)所需的时间。 在这种情况下，为了响应向工作状态 S0 返回系统的系统集电源 IRP，设备电源策略所有者应执行以下一系列操作：

1.  在为驱动程序的[DispatchPower 例程](dispatchpower-routines.md)中的 S0 系统电源状态收到**irp \_ MN \_ 设置 \_ 电源**irp 后，为 IRP 设置*IoCompletion*例程，并将 irp 向下传递到堆栈。

2.  在步骤 (1) 中设置的 *IoCompletion* 例程中，请求 IRP MN 为相应的设备电源状态 ** \_ \_ 设置 \_ 电源** irp，然后立即完成系统设置-POWER irp。 驱动程序在完成系统设置-power IRP 之前，不应等待设备设置-电源 Irp 完成。 *IoCompletion*例程在所有较低级别的驱动程序完成后执行。系统设置-power irp，系统集-电源 irp 会传递回驱动程序的功能设备对象 (FDO) 。

3.  执行任何所需的特定于设备的初始化。

4.  完成在步骤 (2) 中发送的设备设置电源 IRP。

5.  当设备处于 [设备睡眠状态](device-sleeping-states.md)时，处理排队的 i/o 请求。

内核电源管理器具有一组有限的 IRP 调度队列，必须快速通知系统中的所有设备返回到系统工作状态 S0。 未能尽快完成系统集电源 IRP 的驱动程序会阻止其他设备获取其系统设置-power IRP，这可能会对系统电源状态转换过程中的整体系统性能产生负面影响。

有关处理系统设置-电源 Irp 的详细信息，请参阅以下内容：

[确定正确的设备电源状态](determining-the-correct-device-power-state.md)

[在系统 Set-Power IRP 响应中发送设备 Set-Power IRP](sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp.md)

 

