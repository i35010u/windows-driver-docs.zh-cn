---
title: SCSI 端口 I/O 模型
description: SCSI 端口 I/O 模型
ms.assetid: c79fdc99-30ae-4c4a-a130-2b8743bbff7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7abd328efbd44c8ad0b77d9d672de5a1ce3d0ea4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363358"
---
# <a name="scsi-port-io-model"></a>SCSI 端口 I/O 模型


## <span id="ddk_scsi_port_i_o_model_kg"></span><span id="DDK_SCSI_PORT_I_O_MODEL_KG"></span>


SCSI 端口驱动程序通过指向其调度表和驱动程序对象中的微型端口驱动程序回调例程的指针的一系列与其微型端口驱动程序进行通信。 微型端口驱动程序调用[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)才能初始化 SCSI 端口的调度例程表和驱动程序具有这些回调指针的对象。 一个此类回调指针是用来处理 I/O 请求的微型端口驱动程序的启动 I/O 例程的入口点。 端口驱动程序分配到此指针**DriverStartIo**驱动程序对象的成员。

SCSI 端口接收来自更高级别的驱动程序的 I/O 请求，只要它在内部队列中的对请求进行排队。 SCSI 端口的内部队列的详细信息，请参阅[SCSI 端口驱动程序的队列管理](scsi-port-driver-s-queue-management.md)。

SCSI 端口目标设备已准备好接收下一步的 I/O 请求后，调用[ **IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)，从而又会调用微型端口驱动程序启动 I/O 回调例程，存储在**DriverObject-&gt;DriverStartIo**。 有关操作和必须具备以下特征的微型端口驱动程序的启动 I/O 例程的信息，请参阅[SCSI 微型端口驱动程序 HwScsiStartIo 例程](scsi-miniport-driver-s-hwscsistartio-routine.md)。

SCSI 端口调用微型端口驱动程序的启动 I/O 例程，以屏蔽出中断并保证开始 I/O 例程同步对关键的操作系统和驱动程序结构的访问之前引发处理器的 IRQL。

存储类驱动程序和 SCSI 端口驱动程序之间的 I/O 请求数据包流是异步的而是同步的 SCSI 端口驱动程序和目标设备之间的 I/O 请求数据包的流。 SCSI 端口使用内部队列系统，从而能够将新的 I/O 请求发送到 SCSI 端口之前完成以前的 I/O 请求的类驱动程序。 但是，SCSI 端口不发送下一步的 I/O 请求到目标设备直到微型端口驱动程序微型端口驱动程序已准备好接收下一步的 I/O 请求中收到通知。 微型端口驱动程序会通过调用通知 SCSI 端口[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)库例程。

Storport 驱动程序提供更灵活的 I/O 模型，特别是对于中断的屏蔽。 Storport I/O 模型和 SCSI 端口 I/O 模型之间的差异的信息，请参阅[Storport I/O 模型](storport-i-o-model.md)。

 

 




