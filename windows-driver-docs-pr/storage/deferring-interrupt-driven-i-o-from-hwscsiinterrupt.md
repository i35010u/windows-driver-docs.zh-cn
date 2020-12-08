---
title: 延迟 HwScsiInterrupt 中的中断驱动型 I/O
description: 延迟 HwScsiInterrupt 中的中断驱动型 I/O
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiInterrupt
- HwScsiInterrupt
- 中断 WDK SCSI
- 延迟中断驱动 i/o WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3d59bda6275576d3b27a00b924d35cdcbbf44fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835353"
---
# <a name="deferring-interrupt-driven-io-from-hwscsiinterrupt"></a>延迟 HwScsiInterrupt 中的中断驱动型 I/O


## <span id="ddk_deferring_interrupt_driven_i_o_from_hwscsiinterrupt_kg"></span><span id="DDK_DEFERRING_INTERRUPT_DRIVEN_I_O_FROM_HWSCSIINTERRUPT_KG"></span>


如果中断驱动的 i/o 操作需要很长时间才能完成，则微型端口驱动程序应包含一对 [**HwScsiEnableInterruptsCallback**](/previous-versions/windows/hardware/drivers/ff557295(v=vs.85)) 和 [**HwScsiDisableInterruptsCallback**](/previous-versions/windows/hardware/drivers/ff557288(v=vs.85)) 例程。

例如，如果微型端口驱动程序的运行时间不能超过50微秒，则其 *HwScsiInterrupt* 例程 *不* 应保持对 CPU 的控制，以完成请求的操作。 相反，它的 *HwScsiInterrupt* 例程应该执行以下操作：

1.  禁用 HBA 的中断。

2.  设置设备扩展，其中包含完成操作所需的任何上下文。

3.  调用 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) ，其中包含指向设备扩展、* NotificationType ***CallEnableInterrupts** 和微型端口驱动程序的 *HwScsiEnableInterruptsCallback* 例程的指针，如 [SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md)所述。

4.  返回控件。

**ScsiPortNotification** 例程将 *HWSCSIENABLEINTERRUPTSCALLBACK* 例程作为 DPC 例程调用。 有关 Dpc 的详细信息，请参阅 [Dpc 对象和 dpc](../kernel/introduction-to-dpc-objects.md)。

如果微型端口驱动程序的 *HwScsiInterrupt* 例程无法禁用 HBA 上的中断，但其中断驱动的传输在 *HwScsiInterrupt* 例程中可能需要超过50微秒，则驱动程序编写器应通过限制其接受的传输大小来优化微型端口驱动程序。 否则，每次微小型驱动程序同时传输数据时，鼠标指针将显示 "jumpy" 和/或串行和并行吞吐量。

此类微型端口驱动程序的 *HwScsiFindAdapter* 例程应将端口配置信息中的 **MaximumTransferLength** 值重置 \_ \_ 为允许微型端口驱动程序执行中断驱动的传输的值，而不会明显影响其他系统驱动程序的性能。

此类微型端口驱动程序还可能使用微型端口驱动程序提供的 *HwScsiTimer* 例程来调用 **ScsiPortNotification** 。 有关与 *HwScsiInterrupt* 例程同步的 *HwScsiTimer* 例程的详细信息，请参阅 [SCSI 微型端口驱动程序的 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

