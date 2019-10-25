---
title: 处理设备电源策略所有者中的系统 Set-Power IRP
description: 处理设备电源策略所有者中的系统 Set-Power IRP
ms.assetid: f6206455-142b-4f3f-ae5a-d8e79386bce3
keywords:
- 设置电源 Irp WDK 电源管理
- 设备电源策略所有者 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6f471152bd518fdd52f9944b221c99d09f2078
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836614"
---
# <a name="handling-a-system-set-power-irp-in-a-device-power-policy-owner"></a>处理设备电源策略所有者中的系统 Set-Power IRP





为了响应系统设置-电源 IRP，设备堆栈的[电源策略所有者](managing-device-power-policy.md)负责将其设备堆栈置于适当的设备电源状态。

通常，当设备电源策略所有者收到[**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)为系统电源状态设置\_电源时，它应通过将系统设置-电源 IRP 向下传递到设备堆栈来做出响应。 设备电源策略所有者还应通过向下发送设备堆栈 IRP 来做出响应 **\_MN\_设置** [*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中相应设备电源状态的\_电源。 堆栈中的所有驱动程序都完成设备设置-电源 IRP 后，设备电源策略所有者完成系统设置-power IRP。

但是，为了提高系统恢复性能，没有子设备的设备的设备电源所有者应使用不同的方法来减少系统从[睡眠状态](system-sleeping-states.md)返回到[工作状态 S0](system-working-state-s0.md)所需的时间。 在这种情况下，为了响应向工作状态 S0 返回系统的系统集电源 IRP，设备电源策略所有者应执行以下一系列操作：

1.  收到**irp\_MN 后\_** 在驱动程序的[DispatchPower 例程](dispatchpower-routines.md)中为 S0 系统电源状态设置\_电源 IRP，并为 irp 设置*IoCompletion*例程，并向下传递 irp。

2.  在步骤（1）中的*IoCompletion*例程中，请求**IRP\_MN\_将\_电源 IRP 设置**为相应的设备电源状态，然后立即完成系统设置-POWER IRP。 驱动程序在完成系统设置-power IRP 之前，不应等待设备设置-电源 Irp 完成。 在所有较低级别的驱动程序完成了系统设置-power IRP 并且系统集-电源 IRP 传递回驱动程序的功能设备对象（FDO）后，将执行*IoCompletion*例程。

3.  执行任何所需的特定于设备的初始化。

4.  完成在步骤中发送的设备设置电源 IRP （2）。

5.  当设备处于[设备睡眠状态](device-sleeping-states.md)时，处理排队的 i/o 请求。

内核电源管理器具有一组有限的 IRP 调度队列，必须快速通知系统中的所有设备返回到系统工作状态 S0。 未能尽快完成系统集电源 IRP 的驱动程序会阻止其他设备获取其系统设置-power IRP，这可能会对系统电源状态转换过程中的整体系统性能产生负面影响。

有关处理系统设置-电源 Irp 的详细信息，请参阅以下内容：

[确定正确的设备电源状态](determining-the-correct-device-power-state.md)

[发送设备集-电源 IRP 以响应系统设置-Power IRP](sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp.md)

 

 




