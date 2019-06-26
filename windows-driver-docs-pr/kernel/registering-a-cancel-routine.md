---
title: 注册 Cancel 例程
description: 注册 Cancel 例程
ms.assetid: ebc63fb6-bf4d-4de3-9232-08d810c2f730
keywords:
- 正在取消 Irp，注册取消例程
- 取消例程注册
- 注册取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c514e4e81df7ff4c29b2bbbe10961f3fd8343e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378729"
---
# <a name="registering-a-cancel-routine"></a>注册 Cancel 例程





如果设备驱动程序有[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，可以注册其调度例程[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程通过提供其地址为输入到[ **IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)。

如果驱动程序不具有*StartIo*例程，其调度例程必须执行以下操作之前队列 IRP 中以便做进一步的处理其他驱动程序例程：

1.  调用[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  调用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)输入 IRP 和驱动程序提供的入口点*取消*例程。

3.  调用[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))。

有关取消自旋锁的信息，请参阅[使用系统的取消自旋锁](using-the-system-s-cancel-spin-lock.md)。

管理其自己的 Irp，而不是使用 I/O 管理器提供的设备队列，队列的驱动程序不需要调用时获取取消自旋锁**IoSetCancelRoutine**。 但是，这些驱动程序，应检查*取消*例程的指针的**IoSetCancelRoutine**返回以确定是否*取消*例程已启动。

 

 




