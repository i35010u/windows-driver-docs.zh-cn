---
title: 锁定 SCSI 端口驱动程序的内部队列
description: 锁定 SCSI 端口驱动程序的内部队列
ms.assetid: ea5be4e1-4908-431c-9c80-96539157b87e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e938816dd8fa1ef0db51995733118bcac7199012
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519171"
---
# <a name="locking-scsi-port-drivers-internal-queue"></a>锁定 SCSI 端口驱动程序的内部队列


## <span id="ddk_locking_scsi_port_driver_s_internal_queue_kg"></span><span id="DDK_LOCKING_SCSI_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


在类驱动程序和其他更高级别的驱动程序可以强制 SCSI 端口来暂停其队列中请求的处理。 在类驱动程序通过将其发送类型 SRB SRB 暂停 SCSI Port 的队列\_函数\_锁\_队列。 在类驱动程序通常会中止更改设备的电源状态，以便在 SCSI Port 的队列中请求的处理。 更改设备的电源状态之后, 的类驱动程序对队列进行解锁。 序列是按如下所示：

1.  类驱动程序锁定 SCSI Port 的队列 (使用 IRP\_MJ\_SRB SRB 函数值的 SCSI\_函数\_锁\_队列)。

2.  类驱动程序请求的电源状态更改 (使用 IRP\_MJ\_SRB 使用 SCSI\_标志\_绕过\_已锁定\_队列标志设置，以确保未排队 IRP 幂)。

3.  类驱动程序解锁 SCSI Port 的队列 (IRP\_MJ\_SRB SRB 函数值的 SCSI\_函数\_解锁\_队列和 SRB\_标志\_绕过\_锁定\_队列标志设置)。

解锁其队列后，SCSI 端口恢复处理排队的 Srb。 类驱动程序不应尝试绕过已被另一个驱动程序锁定的队列。

有关从类驱动程序的角度来看解锁队列的详细信息，请参阅[存储类驱动程序 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)。

 

 




