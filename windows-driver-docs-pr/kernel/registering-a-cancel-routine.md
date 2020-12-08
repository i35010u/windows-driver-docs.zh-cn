---
title: 注册 Cancel 例程
description: 注册 Cancel 例程
keywords:
- 取消 Irp，注册取消例程
- 取消例程，注册
- 注册取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fa13beb81d5458a40801e164fdb84921f0d105b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837995"
---
# <a name="registering-a-cancel-routine"></a>注册 Cancel 例程





如果设备驱动程序具有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则其调度例程可以通过将其地址作为输入提供给 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)来注册 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。

如果驱动程序没有 *StartIo* 例程，则其调度例程必须执行以下操作，然后再将 IRP 排队，以便进一步处理其他驱动程序例程：

1.  调用 [**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  使用输入 IRP 和驱动程序提供的 *取消* 例程的入口点调用 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 。

3.  调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))。

有关 "取消旋转锁定" 的信息，请参阅 [使用系统的 "取消旋转" 锁](using-the-system-s-cancel-spin-lock.md)。

用于管理自己的 Irp 队列的驱动程序（而不是使用 i/o 管理器提供的设备队列），无需在调用 **IoSetCancelRoutine** 时获取 cancel 自旋锁。 但是，这些驱动程序应检查 **IoSetCancelRoutine** 返回的 *取消* 例程指针，以确定 *取消* 例程是否已启动。

 

