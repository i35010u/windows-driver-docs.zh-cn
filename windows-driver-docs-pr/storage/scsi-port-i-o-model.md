---
title: SCSI 端口 I/O 模型
description: SCSI 端口 I/O 模型
ms.assetid: c79fdc99-30ae-4c4a-a130-2b8743bbff7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c87f3c9203e3ab07955c6f9f6163c8b39278ddc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842657"
---
# <a name="scsi-port-io-model"></a>SCSI 端口 I/O 模型


## <span id="ddk_scsi_port_i_o_model_kg"></span><span id="DDK_SCSI_PORT_I_O_MODEL_KG"></span>


SCSI 端口驱动程序通过其调度表和驱动程序对象中的一系列指向微型端口驱动程序回调例程的指针，与其微型端口驱动程序通信。 微型端口驱动程序从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize) ，以便用这些回调指针初始化 SCSI 端口的调度表和驱动程序对象。 一个此类回调指针是用于处理 i/o 请求的微型端口驱动程序的启动 i/o 例程的入口点。 端口驱动程序将此指针分配给驱动程序对象的**DriverStartIo**成员。

当 SCSI 端口接收到来自较高级别的驱动程序的 i/o 请求时，它会将请求排队到内部队列中。 有关 SCSI 端口的内部队列的详细信息，请参阅[Scsi 端口驱动程序的队列管理](scsi-port-driver-s-queue-management.md)。

一旦目标设备准备好接收下一个 i/o 请求，SCSI 端口就会调用[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)，后者又会调用**DriverObject&gt;DriverStartIo**中存储的微型端口驱动程序启动 i/o 回调例程。 有关微型端口驱动程序启动 i/o 例程的操作和所需特征的信息，请参阅[SCSI 微型端口驱动程序的 HwScsiStartIo 例程](scsi-miniport-driver-s-hwscsistartio-routine.md)。

在调用微型端口驱动程序的启动 i/o 例程之前，SCSI 端口会引发处理器的 IRQL，以便屏蔽中断，并确保启动 i/o 例程已同步访问关键操作系统和驱动程序结构。

尽管存储类驱动程序和 SCSI 端口驱动程序之间的 i/o 请求数据包流是异步的，但 SCSI 端口驱动程序和目标设备之间的 i/o 请求流是同步的。 SCSI 端口使用内部队列系统，使类驱动程序可以在前一个 i/o 请求完成之前向 SCSI 端口发送新的 i/o 请求。 但是，SCSI 端口不会将下一个 i/o 请求发送到目标设备，直到它收到来自微型端口驱动程序的通知，使微型端口驱动程序可以接收下一个 i/o 请求。 微型端口驱动程序调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)库例程，通知 SCSI 端口。

Storport 驱动程序提供了更灵活的 i/o 模型，特别是在出现中断的情况下。 有关 Storport i/o 模型与 SCSI 端口 i/o 模型之间的差异的信息，请参阅[storport I/o 模型](storport-i-o-model.md)。

 

 




