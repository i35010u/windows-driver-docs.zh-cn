---
title: 设备电源 IRP 的 IoCompletion 例程
description: 设备电源 IRP 的 IoCompletion 例程
ms.assetid: c275fcba-5fa9-427c-8d7e-2339563985e4
keywords:
- IoCompletion 例程
- power Irp WDK 内核，设备更改
- 状态转换 WDK 电源管理
- 设备状态转换 WDK 电源管理
- 工作状态返回 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d97dd80cc93544f0aa161ae40b8564e99cce5dd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183995"
---
# <a name="iocompletion-routines-for-device-power-irps"></a>设备电源 IRP 的 IoCompletion 例程





在总线驱动程序完成 IRP 后，当 i/o 管理器将 IRP 向下传递到堆栈中时，它会调用由较高级别的驱动程序注册的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

每当设备进入 D0 状态时，其每个驱动程序都应该设置一个 *IoCompletion* 例程，用于执行将其返回到工作状态所需的大部分任务。 对于任何到 D0 状态的转换，驱动程序都应该设置 *IoCompletion* 例程，无论设备是从睡眠状态返回，还是在系统启动时输入 D0 都是如此。 下图显示了 *IoCompletion* 例程应执行的任务。

![说明设备开机 iocompletion 例程的示意图](images/d0-comp.png)

这些任务包括：

-   根据需要还原设备电源状态或重新初始化设备，并准备在设备未处于工作状态时处理驱动程序排队的任何 i/o

-   调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器设备处于 D0 电源状态。

-   如果驱动程序最初未发送当前的 power IRP，则调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 以接收下一个 power irp。 仅)  (Windows Server 2003、Windows XP 和 Windows 2000。

-   释放分配给设备上下文的内存。

-   调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) ，以释放驱动程序收到 IRP 时在其 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中获取的锁。

-   返回状态 \_ 成功。

总线驱动程序不会开启设备，直到设备或更高版本的驱动程序必须与设备通信。

当其设备进入睡眠状态时，驱动程序应设置 *IoCompletion* 例程，该例程将调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) (仅) Windows SERVER 2003、windows XP 和 windows 2000，并释放删除锁定。 请记住，在设备处于睡眠状态时，驱动程序无法访问其设备。

 

