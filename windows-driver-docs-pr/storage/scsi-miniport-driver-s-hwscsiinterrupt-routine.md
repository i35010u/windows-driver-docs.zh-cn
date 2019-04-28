---
title: SCSI 微型端口驱动程序的 HwScsiInterrupt 例程
description: SCSI 微型端口驱动程序的 HwScsiInterrupt 例程
ms.assetid: 8760e7e4-1721-4e55-99e6-c9e234368fa1
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiInterrupt
- HwScsiInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044e7e95950cd724feda8b59eb1ca47256fcec0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354557"
---
# <a name="scsi-miniport-drivers-hwscsiinterrupt-routine"></a>SCSI 微型端口驱动程序的 HwScsiInterrupt 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiinterrupt_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINTERRUPT_ROUTINE_KG"></span>


在进入时， [ **HwScsiInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff557312)例程应确定其 HBA 是否实际生成中断。 *HwScsiInterrupt*必须返回**FALSE**越早越好如果它检测到虚假的中断，因此可以快速调用 ISR 实际生成中断的设备。

否则为微型端口驱动程序*HwScsiInterrupt*例程程序通常负责完成 I/O 操作导致中断。 具体取决于 HBA 和的微型端口驱动程序，设计*HwScsiInterrupt*例程会执行一些或所有以下：

-   解除 HBA （必需） 上中断

-   通知端口驱动程序 (通过调用[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)或[ **ScsiPortCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff564608)) 如果 HBA 指明某些 SCSI 错误条件操作过程中发生，并可能会将错误记录。

    有关日志记录错误的详细信息，请参阅[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)。

-   完成请求的操作导致的中断，例如，调用[ **ScsiPortIoMapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff564649) (请参阅[SCSI 微型端口驱动程序 HwScsiDmaStarted 例程](scsi-miniport-driver-s-hwscsidmastarted-routine.md)) 如果中断来自以前选定的目标 TID 和 LU，指示已准备好将数据传输。

当*HwScsiInterrupt*例程 （或内部的微型端口驱动程序例程） 完成 SRB，它将调用**ScsiPortNotification**两次：

1.  首先，由于*NotificationType * * * RequestComplete** 和只满足 SRB。

2.  接下来，使用 * NotificationType ***NextRequest**，或使用**NextLuRequest**如果 HBA 支持有标记的队列或每个逻辑单元的多个请求。

为了更好地整体系统性能，微型端口驱动程序的*HwScsiInterrupt*例程应执行的操作仅处理 I/O 请求所需的最低。 也就是说，微型端口驱动程序应设计为返回控件从*HwScsiInterrupt*尽可能快地例程。 *HwScsiInterrupt*不能调用例程[ **ScsiPortStallExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff564757)与较大的时间间隔，从而占用处理器和阻止从其他驱动程序服务及其设备中断。

 

 




