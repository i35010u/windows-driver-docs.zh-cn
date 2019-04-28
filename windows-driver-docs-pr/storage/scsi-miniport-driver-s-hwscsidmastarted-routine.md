---
title: SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程
description: SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程
ms.assetid: 697839f0-e912-42a5-abe0-f6bb946c86d8
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiDmaStarted
- HwScsiDmaStarted
- DMA 控制器 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08b155914ad17e34ffa8f840b066a323f1a9d715
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339936"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI 微型端口驱动程序的 HwScsiDmaStarted 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidmastarted_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDMASTARTED_ROUTINE_KG"></span>


使用系统 DMA 控制器的 HBA 的微型端口驱动程序必须具有[ **HwScsiDmaStarted** ](https://msdn.microsoft.com/library/windows/hardware/ff557291)例程。

对于数据传输操作中，这样的微型端口驱动程序必须调用[ **ScsiPortIoMapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff564649)、 传入到每个 HBA 数据其设备扩展和请求传输，以及 SRB 的指针使用的缓冲区的数据会传输到或从其逻辑地址范围。

请注意，逻辑地址范围传递到**ScsiPortIoMapTransfer**必须是输入 SRB 的映射的值**DataBuffer**并**DataTransferLength**或此范围的真子集。 对于大多数传输请求，微型端口驱动程序编写器可以假定输入 SRB 中指定的所有数据，可以都传输单个 DMA 操作。

具体而言，微型端口驱动程序可能需要执行多个从属的 DMA 传输操作，以满足给定的 SRB，仅当 HBA 提供应用程序专用的支持，且应用程序直接向微型端口驱动程序发送大型传输请求. 否则为它负责存储类驱动程序来拆分为分部传输请求一组大型传输请求，每个大小调整，以满足 HBA 的功能 (请参阅[存储类驱动程序](storage-class-drivers.md))。

**ScsiPortIoMapTransfer**微型端口驱动程序将调用*HwScsiDmaStarted*例程时系统 DMA 控制器已准备好系统内存和 HBA 之间传输数据。 *HwScsiDmaStarted*必须设置在传输操作的 HBA。

传输操作完成后，必须调用微型端口驱动程序[ **ScsiPortFlushDma** ](https://msdn.microsoft.com/library/windows/hardware/ff564618)调用之前**ScsiPortNotification** SRB 和/或调用**ScsiPortIoMapTransfer**设置子范围中的应用程序提供的缓冲区再次的 DMA 控制器，如果 HBA 专用于在用户模式应用程序的支持。

**ScsiPortFlushDma**刷新缓存在 DMA 控制器中的任何剩余数据。 请注意， **ScsiPortFlushDma**还可以调用以进行取消系统 DMA 传输，即使微型端口驱动程序*HwScsiDmaStarted*尚未调用例程。

请参阅[ **ScsiPortIoMapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff564649)并[ **ScsiPortFlushDma** ](https://msdn.microsoft.com/library/windows/hardware/ff564618)有关详细信息。

 

 




