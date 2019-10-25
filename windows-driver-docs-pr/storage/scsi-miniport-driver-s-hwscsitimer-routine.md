---
title: SCSI 微型端口驱动程序的 HwScsiTimer 例程
description: SCSI 微型端口驱动程序的 HwScsiTimer 例程
ms.assetid: 57ac7a6e-ada5-4185-89cf-b6c5ef9006d4
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiTimer
- HwScsiTimer
- 计时器，WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a327103c9cb2151a27724e357b28089f8621cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842661"
---
# <a name="scsi-miniport-drivers-hwscsitimer-routine"></a>SCSI 微型端口驱动程序的 HwScsiTimer 例程


## <span id="ddk_scsi_miniport_drivers_hwscsitimer_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSITIMER_ROUTINE_KG"></span>


无[**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))例程的微型端口驱动程序，因为它通过轮询管理所有 HBA i/o 操作，因此应具有[*HwScsiTimer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557327(v=vs.85))例程。 但是， *HwScsiInterrupt*例程的小型小型驱动程序通常也有*HwScsiTimer*例程。

当微型端口驱动程序可以调用[**ScsiPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportstallexecution)来等待 HBA 上的状态更改时，微型端口驱动程序*不*应调用此例程等待超过一毫秒，只是在正在初始化微型端口驱动程序。 **ScsiPortStallExecution**在给定的时间间隔内建立处理器的联系，阻止系统中的其他代码执行有用的工作。

微型端口驱动程序应具有*HwScsiTimer*例程，而不是在输入间隔较大的情况下调用**ScsiPortStallExecution**并浪费许多 CPU 周期。 如果 HBA 不会为每个操作生成完成中断，或者任何常请求的操作（如总线重置）所需的时间超过毫秒，则一个或多个*HwScsiTimer*例程特别有用。

为此类操作对 HBA 进行编程后，微型端口驱动程序将使用 * NotificationType ***RequestTimerCall**调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) ，该指针指向包含操作上下文的特定于 HBA 的设备扩展。它的*HwScsiTimer*入口点和驱动程序确定的间隔。

**ScsiPortNotification**会将对*HwScsiTimer*例程的调用与*HwScsiInterrupt*例程同步，以使*HwScsiTimer*例程运行时无法并发执行。

对于调用**ScsiPortNotification**的每个调用，将调用*HwScsiTimer*一次，该调用可从*HwScsiTimer*例程本身调用。 但是，使用*NotificationType * * * RequestTimerCall** 对**ScsiPortNotification**进行的任何调用会替代前面的调用，指定的间隔尚未过期。 也就是说，在任何给定时刻，都只有一个未完成的请求可调用微型端口驱动程序的*HwScsiTimer*例程。

传递给**ScsiPortNotification**的时间间隔以微秒为单位，每次调用*HwScsiTimer*例程的最小开销大约为10微秒。 如果输入间隔为零，则会取消上述请求调用*HwScsiTimer*例程，前提是未调用或分派在基于 NT 的 SMP 计算机的另一个处理器上执行。

 

 




