---
title: SCSI 微型端口驱动程序的 HwScsiTimer 例程
description: SCSI 微型端口驱动程序的 HwScsiTimer 例程
ms.assetid: 57ac7a6e-ada5-4185-89cf-b6c5ef9006d4
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiTimer
- HwScsiTimer
- 计时器 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21b4b2fcbe61e07822dfe67e776dc2d5d3738acb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386493"
---
# <a name="scsi-miniport-drivers-hwscsitimer-routine"></a>SCSI 微型端口驱动程序的 HwScsiTimer 例程


## <span id="ddk_scsi_miniport_drivers_hwscsitimer_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSITIMER_ROUTINE_KG"></span>


微型端口驱动程序，但没有[ **HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))例程因为它通过轮询来管理所有 HBA I/O 操作应具有[ *HwScsiTimer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557327(v=vs.85))例程。 但是，具有的微型端口驱动程序*HwScsiInterrupt*例程经常会有*HwScsiTimer*也例程。

尽管微型端口驱动程序可以调用[ **ScsiPortStallExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportstallexecution) HBA 上等待的状态更改，微型端口驱动程序应*永远不会*调用该例程要等待的时间更长除一毫秒，比可能是，对于操作执行仅在初始化微型端口驱动程序时。 **ScsiPortStallExecution**给定间隔内，在系统中阻止执行有用的工作的其他代码占用处理器。

而不是调用**ScsiPortStallExecution**微型端口驱动程序应具有较大输入的时间间隔和浪费多 CPU 周期， *HwScsiTimer*例程。 一个或多个*HwScsiTimer*如果 HBA 不会生成每个操作的完成中断或任何通常请求的操作，例如总线重置，花费的时间超过一毫秒以下，例程是特别有用。

HBA 具有已设计用来实现此类操作后，微型端口驱动程序会调用[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)与 * NotificationType ***RequestTimerCall**、指向包含有关此操作，上下文其特定于 HBA 的设备扩展其*HwScsiTimer*入口点和驱动程序确定的间隔。

**ScsiPortNotification**同步调用*HwScsiTimer*例程替换为那些*HwScsiInterrupt* ，以便它不能执行例程同时而*HwScsiTimer*运行例程。

*HwScsiTimer*调用一次到每个此类调用**ScsiPortNotification**，可以从调用*HwScsiTimer*例程本身。 但是，任何对**ScsiPortNotification**与*NotificationType * * * RequestTimerCall** 重写前面为其指定的时间间隔未过期调用。 也就是说，没有要调用的微型端口驱动程序只有一个未完成请求*HwScsiTimer*例程在任何给定时间点。

在间隔中传递给**ScsiPortNotification**处于 （毫秒），每次调用的开销最小*HwScsiTimer*例程是大约 10 个微秒为单位。 输入的间隔为零将取消上一个请求来调用*HwScsiTimer*例程中，提供它尚未调用或调度为基于 NT 的 SMP 计算机中的另一个处理器上执行。

 

 




