---
title: 延迟 HwScsiInterrupt 中的中断驱动型 I/O
description: 延迟 HwScsiInterrupt 中的中断驱动型 I/O
ms.assetid: 6bedad0c-8995-4c7b-8ee2-415ec63e0eb3
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiInterrupt
- HwScsiInterrupt
- 中断 WDK SCSI
- 延迟的中断驱动 I/O WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b358d5adf70961f65ebcc04cd52256b9f280ddcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344970"
---
# <a name="deferring-interrupt-driven-io-from-hwscsiinterrupt"></a>延迟 HwScsiInterrupt 中的中断驱动型 I/O


## <span id="ddk_deferring_interrupt_driven_i_o_from_hwscsiinterrupt_kg"></span><span id="DDK_DEFERRING_INTERRUPT_DRIVEN_I_O_FROM_HWSCSIINTERRUPT_KG"></span>


如果中断驱动 I/O 操作需要很长时间才能完成，微型端口驱动程序应具有一对[ **HwScsiEnableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557295)并[ **HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)例程。

例如，如果微型端口驱动程序必须停止的时间超过 50 微秒为单位进行 PIO，其*HwScsiInterrupt*例程应*不*保留完整的 CPU 的控制的轮询间隔来完成请求的操作。 相反，其*HwScsiInterrupt*例程应执行以下操作：

1.  禁用来自 HBA 的中断。

2.  设置与任何上下文设备扩展所需完成此操作。

3.  调用[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)用一个指针指向设备扩展，* NotificationType ***CallEnableInterrupts**，和微型端口驱动程序的*HwScsiEnableInterruptsCallback*例程中, 所述[SCSI 微型端口驱动程序 HwScsiEnableInterruptsCallback 例程](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md)。

4.  返回控件。

**ScsiPortNotification**例程调用*HwScsiEnableInterruptsCallback*例程作为 DPC 例程。 有关 dpc 进行标记的详细信息，请参阅[DPC 对象和 dpc 进行标记](https://msdn.microsoft.com/library/windows/hardware/ff544084)。

如果微型端口驱动程序*HwScsiInterrupt*例程不能禁用 HBA 上的中断，但其中断驱动传输可以在中执行多个 50 微秒*HwScsiInterrupt*例程，则驱动程序编写器应通过限制它接受的传输大小调整微型端口驱动程序。 否则为将显示"动摇"鼠标指针和/或每次微型端口驱动程序传输数据的同时，串行和并行吞吐量会显著降低。

这样的微型端口驱动程序的*HwScsiFindAdapter*例程应重置**MaximumTransferLength**端口中的值\_配置\_到允许的值的信息若要执行中断驱动传输而不会显著影响性能的其他系统驱动程序微型端口驱动程序。

这样的微型端口驱动程序还可能会调用**ScsiPortNotification**微型端口驱动程序提供与*HwScsiTimer*例程。 有关详细信息*HwScsiTimer*例程，与同步*HwScsiInterrupt*例程，请参阅[SCSI 微型端口驱动程序 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

 

 




