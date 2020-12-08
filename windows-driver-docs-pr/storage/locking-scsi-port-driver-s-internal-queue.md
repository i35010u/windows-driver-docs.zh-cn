---
title: 锁定 SCSI 端口驱动程序的内部队列
description: 锁定 SCSI 端口驱动程序的内部队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1645a3e6b5a13f4b0ac1ffdc045dbf60eec3225
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835061"
---
# <a name="locking-scsi-port-drivers-internal-queue"></a>锁定 SCSI 端口驱动程序的内部队列


## <span id="ddk_locking_scsi_port_driver_s_internal_queue_kg"></span><span id="DDK_LOCKING_SCSI_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


类驱动程序和其他更高级别的驱动程序可以强制 SCSI 端口暂停处理其队列中的请求。 类驱动程序通过向其发送 SRB \_ 函数锁定队列类型的 SRB 来停止 SCSI 端口的队列 \_ \_ 。 类驱动程序通常会阻止处理 SCSI 端口的队列中的请求，从而更改设备的电源状态。 更改设备的电源状态后，类驱动程序会解锁队列。 顺序如下：

1.  类驱动程序使用 IRP MJ SCSI 锁定 SCSI 端口的队列 (\_ \_ ，其 SRB 函数值为 SRB \_ function \_ LOCK \_ queue) 。

2.  类驱动程序请求更改电源状态 (使用 IRP \_ MJ \_ SCSI，并设置了 SRB \_ 标志 \_ 旁路 \_ 锁定 \_ 队列标志，以确保 power IRP 未排队) 。

3.  类驱动程序解锁 SCSI 端口的队列 (IRP \_ MJ \_ SCSI，SRB 函数值为 SRB \_ function \_ UNLOCK \_ queue，并使用 SRB \_ FLAGS \_ 绕过 \_ 锁定 \_ 队列标志集) 。

队列解锁后，SCSI 端口会恢复处理排队 SRBs。 类驱动程序不应尝试绕过被其他驱动程序锁定的队列。

有关从类驱动程序的角度对队列进行解锁的详细信息，请参阅 [存储类驱动程序的 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)。

 

 




