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
ms.openlocfilehash: 120dacfaf8252bbc4b6c56a416d669c447df1622
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188487"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程

使用系统 DMA 控制器的 HBA 的微型端口驱动程序必须具有 [**HwScsiDmaStarted**](/previous-versions/windows/hardware/drivers/ff557291(v=vs.85)) 例程。

对于数据传输操作，此类微型端口驱动程序必须调用 [**ScsiPortIoMapTransfer**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)，将指向其设备扩展的指针传入每 HBA 数据，并传入请求传输的 SRB，以及要从中传输数据的缓冲区的逻辑地址范围。

请注意，传递给 **ScsiPortIoMapTransfer** 的逻辑地址范围必须是输入 SRB 的 **DataBuffer** 和 **DataTransferLength** 的映射值或此范围的正确子集。 对于大多数传输请求，微型端口驱动程序编写器可以假定在输入 SRB 中指定的所有数据都可以在单个 DMA 操作中传输。

特别是，只有当 HBA 提供应用程序专用支持且应用程序直接将大型传输请求发送到微型端口驱动程序时，微型端口驱动程序才必须执行多个从属 DMA 传输操作才能满足给定的 SRB。 否则，存储类驱动程序负责将大型传输请求拆分为一组部分传输请求，每个请求调整为符合 HBA 的功能 (参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)) 。

当系统 DMA 控制器准备好在系统内存和 HBA 之间传输数据时， **ScsiPortIoMapTransfer**将调用微型端口驱动程序的*HwScsiDmaStarted*例程。 *HwScsiDmaStarted* 必须设置 HBA 以进行传输操作。

当传输操作完成后，微型端口驱动程序必须先调用 [**ScsiPortFlushDma**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) ，然后再调用 **ScsiPortNotification** 和 SRB 和/或调用 **ScsiPortIoMapTransfer** ，以便在 HBA 专用于用户模式应用程序支持的情况下为应用程序提供的缓冲区中的子范围再次设置 DMA 控制器。

**ScsiPortFlushDma** 刷新 DMA 控制器中缓存的所有剩余数据。 请注意，即使尚未调用微型端口驱动程序的*HwScsiDmaStarted*例程，也可以调用**ScsiPortFlushDma**来取消系统 DMA 传输。

有关详细信息，请参阅 [**ScsiPortIoMapTransfer**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer) 和 [**ScsiPortFlushDma**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) 。