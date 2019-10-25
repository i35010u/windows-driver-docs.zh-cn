---
title: SCSI 微型端口驱动程序的 HwScsiInterrupt 例程
description: SCSI 微型端口驱动程序的 HwScsiInterrupt 例程
ms.assetid: 8760e7e4-1721-4e55-99e6-c9e234368fa1
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiInterrupt
- HwScsiInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32755817e01e3ab720512ced49d9f9708afe5fbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842667"
---
# <a name="scsi-miniport-drivers-hwscsiinterrupt-routine"></a>SCSI 微型端口驱动程序的 HwScsiInterrupt 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiinterrupt_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINTERRUPT_ROUTINE_KG"></span>


进入时， [**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))例程应确定其 HBA 是否确实生成了中断。 如果*HwScsiInterrupt*检测到虚假中断，则必须尽快返回**FALSE** ，以便可以快速调用实际产生中断的设备的 ISR。

否则，微型端口驱动程序的*HwScsiInterrupt*例程通常负责完成导致中断的 i/o 操作。 根据 HBA 和微型端口驱动程序的设计， *HwScsiInterrupt*例程会执行以下部分或全部操作：

-   消除 HBA 上的中断（必需）

-   如果 HBA 指示在操作过程中发生了某些 SCSI 错误情况并可能记录错误，则通知端口驱动程序（通过调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)或[**ScsiPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportcompleterequest)）。

    有关记录错误的详细信息，请参阅[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)。

-   完成导致中断的请求操作，如调用[**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer) （请参阅[SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程](scsi-miniport-driver-s-hwscsidmastarted-routine.md)）（如果中断来自以前选择的目标 TID 和 LU），指示传输数据的准备情况。

当*HwScsiInterrupt*例程（或内部微型端口驱动程序例程）完成 SRB 时，它将调用**ScsiPortNotification**两次：

1.  首先，提供了*NotificationType * * * RequestComplete** 和刚满足的 SRB。

2.  接下来，对于 * NotificationType ***NextRequest**，或者如果 HBA 支持标记队列或每个逻辑单元多个请求，则为**NextLuRequest** 。

为了获得更好的整体系统性能，微型端口驱动程序的*HwScsiInterrupt*例程只应执行处理 i/o 请求所需的最低要求。 也就是说，应将微型端口驱动程序设计为尽可能快地从*HwScsiInterrupt*例程返回控制权。 *HwScsiInterrupt*例程不能使用较大的间隔调用[**ScsiPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportstallexecution) ，因此会使处理器独占，并阻止其他驱动程序为其设备中断提供服务。

 

 




