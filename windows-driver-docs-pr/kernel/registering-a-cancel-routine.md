---
title: 注册 Cancel 例程
description: 注册 Cancel 例程
ms.assetid: ebc63fb6-bf4d-4de3-9232-08d810c2f730
keywords:
- 取消 Irp，注册取消例程
- 取消例程，注册
- 注册取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc0d922f4beca83746545e8084075667d499a39e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827577"
---
# <a name="registering-a-cancel-routine"></a>注册 Cancel 例程





如果设备驱动程序具有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则其调度例程可以通过将其地址作为输入提供给[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)来注册[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。

如果驱动程序没有*StartIo*例程，则其调度例程必须执行以下操作，然后再将 IRP 排队，以便进一步处理其他驱动程序例程：

1.  调用[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  使用输入 IRP 和驱动程序提供的*取消*例程的入口点调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 。

3.  调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))。

有关 "取消旋转锁定" 的信息，请参阅[使用系统的 "取消旋转" 锁](using-the-system-s-cancel-spin-lock.md)。

用于管理自己的 Irp 队列的驱动程序（而不是使用 i/o 管理器提供的设备队列），无需在调用**IoSetCancelRoutine**时获取 cancel 自旋锁。 但是，这些驱动程序应检查**IoSetCancelRoutine**返回的*取消*例程指针，以确定*取消*例程是否已启动。

 

 




