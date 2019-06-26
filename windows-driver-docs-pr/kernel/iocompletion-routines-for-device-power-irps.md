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
ms.openlocfilehash: 244c56d1fdd835fbb78e7c6dad3785c0f2a28aac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381689"
---
# <a name="iocompletion-routines-for-device-power-irps"></a>设备电源 IRP 的 IoCompletion 例程





总线驱动程序完成 IRP 后，I/O 管理器会调用[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程注册的更高级别的驱动程序为它们通过 IRP 向下堆栈。

只要设备进入 D0 状态时，每个的驱动程序应设置*IoCompletion*例程执行大部分所需将其返回给工作状态的任务。 驱动程序应设置*IoCompletion*例程的任何转换到 D0 状态，是否在设备从返回睡眠状态或在系统启动时输入 D0。 下图显示了任务这种*IoCompletion*例程应执行。

![说明设备强化 iocompletion 例程的关系图](images/d0-comp.png)

这些任务包括：

-   还原设备电源状态或正在该设备，重新初始化为必需的并准备处理任何 I/O 排队的驱动程序中，当设备不处于工作状态

-   调用[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)通知设备处于 D0 电源状态的电源管理器。

-   调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)以接收 IRP 下, 一步的强大功能，如果该驱动程序未最初发送当前 power IRP。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅）。

-   释放分配的设备上下文的内存。

-   调用[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)若要释放的锁的驱动程序中获取其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程时收到了IRP。

-   返回状态\_成功。

总线驱动程序未接通电源的设备直到它或更高版本的驱动程序必须与设备通信。

驱动程序时其设备进入睡眠状态时，应设置*IoCompletion*调用的例程[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) （Windows Server 2003、 Windows XP 和 Windows仅 2000)，并释放删除锁。 请记住，在设备处于休眠状态时，驱动程序无法访问其设备。

 

 




