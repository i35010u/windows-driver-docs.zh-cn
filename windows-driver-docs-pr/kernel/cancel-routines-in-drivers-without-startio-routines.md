---
title: 不包含 StartIo 例程的驱动程序中的 Cancel 例程
description: 不包含 StartIo 例程的驱动程序中的 Cancel 例程
ms.assetid: c6e1a05e-28ed-4f42-8678-55f01303b312
keywords:
- 取消 Irp，StartIo 例程
- 取消例程，StartIo 例程
- StartIo 例程，取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf9658afd1d39a1bb46050a61c78b03258198588
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188633"
---
# <a name="cancel-routines-in-drivers-without-startio-routines"></a>不包含 StartIo 例程的驱动程序中的 Cancel 例程





仅当 Irp 在关联设备队列对象中排队时，i/o 管理器才会在设备对象中维护 **CurrentIrp** 字段。

没有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程的驱动程序将管理其自己的 irp 的内部队列。 在此类驱动程序中，可以使用输入 IRP （既不是输入目标设备对象的**CurrentIrp** ，也不是驱动程序的内部队列中的 IRP）调用[*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。 驱动程序必须维护其自己的状态，即当前正在处理哪个 IRP，并应为其每个队列提供 " *取消* " 例程。 驱动程序的内部队列应为联锁队列，因为必须由 executive 旋转锁保护其内部队列。

调用驱动程序的 *Cancel* 例程时，通常会执行以下操作：

1.  调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))，并通过 ** &gt; irp->cancelirql**。

2.  获取用于保护其联锁队列的旋转锁，并指导队列查找 irp，并将 **irp 设置 &gt; ** 为 **TRUE**。

    -   如果在联锁队列中找到这样的 IRP，取消排队它会释放保护队列的旋转锁，并使用 w 设置 IRP 的 i/o 状态块

        状态 \_ 的状态**Status**为 "已取消"，如果**信息**为零，则启动下一个排队的 IRP，通过取消的 irp 调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，并返回 control

    -   如果找不到这样的 IRP，则 *取消* 例程会释放它所持有的所有旋转锁并返回控制权。

        驱动程序通常假设在 IRP 未排队时，输入 IRP 的 i/o 处理已经开始。

带有 *取消* 例程的驱动程序也可以处理 [**IRP \_ MJ \_ 清理**](./irp-mj-cleanup.md) 请求。 有关**IRP \_ MJ \_ 清理**请求的详细信息，请参阅[*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 。

 

