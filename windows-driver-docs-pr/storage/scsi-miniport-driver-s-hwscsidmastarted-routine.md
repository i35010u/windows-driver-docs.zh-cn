---
title: SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程
description: SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程
ms.assetid: 697839f0-e912-42a5-abe0-f6bb946c86d8
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiDmaStarted
- HwScsiDmaStarted
- DMA 控制器 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f79b6f7b24c3a565e6038a375746de3b72abb1e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842677"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidmastarted_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDMASTARTED_ROUTINE_KG"></span>


使用系统 DMA 控制器的 HBA 的微型端口驱动程序必须具有[**HwScsiDmaStarted**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85))例程。

对于数据传输操作，此类微型端口驱动程序必须调用[**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)，将指针传递到其设备扩展以获取每 HBA 数据，并传入请求传输的 SRB，以及缓冲区的一系列逻辑地址，其中数据将传输到的或。

请注意，传递给**ScsiPortIoMapTransfer**的逻辑地址范围必须是输入 SRB 的**DataBuffer**和**DataTransferLength**的映射值或此范围的正确子集。 对于大多数传输请求，微型端口驱动程序编写器可以假定在输入 SRB 中指定的所有数据都可以在单个 DMA 操作中传输。

特别是，小型端口驱动程序可能需要执行多个从属 DMA 传输操作，以便仅当 HBA 提供应用程序专用支持且应用程序直接将大型传输请求发送到微型端口驱动程序时才满足给定的 SRB. 否则，存储类驱动程序负责将大型传输请求拆分为一组部分传输请求，每个请求调整大小以适应 HBA 的功能（请参阅[存储类驱动程序](storage-class-drivers.md)）。

当系统 DMA 控制器准备好在系统内存和 HBA 之间传输数据时， **ScsiPortIoMapTransfer**将调用微型端口驱动程序的*HwScsiDmaStarted*例程。 *HwScsiDmaStarted*必须设置 HBA 以进行传输操作。

传输操作完成后，微型端口驱动程序必须先调用[**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) ，然后再调用**ScsiPortNotification**和 SRB 和/或调用**ScsiPortIoMapTransfer** ，为中的子范围再次设置 DMA 控制器如果 HBA 专用于用户模式应用程序的支持，则为应用程序提供的缓冲区。

**ScsiPortFlushDma**刷新 DMA 控制器中缓存的所有剩余数据。 请注意，即使尚未调用微型端口驱动程序的*HwScsiDmaStarted*例程，也可以调用**ScsiPortFlushDma**来取消系统 DMA 传输。

有关详细信息，请参阅[**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)和[**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) 。

 

 




