---
title: 存储类驱动程序的 IoCompletion 例程
description: 存储类驱动程序的 IoCompletion 例程
ms.assetid: 03cf50be-1b7d-4e5b-8ee5-bbdef860d893
keywords:
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9747be4f8e0fea0eb5f623a355069e79f0b98e92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845632"
---
# <a name="storage-class-drivers-iocompletion-routines"></a>存储类驱动程序的 IoCompletion 例程


## <span id="ddk_storage_class_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


存储类驱动程序必须具有一个或多个[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，除非驱动程序以同步方式等待它发送到端口驱动程序的每个 IRP 完成，并根据需要重试请求，然后从调度*中释放 SRBs 的内存，然后BuildRequest*例程。 请注意，同步处理每个 IRP 会降低类驱动程序的性能。 而且，可能包含系统页面文件的设备的存储类驱动程序必须异步处理所有传输请求，因此必须为读/写请求提供*IoCompletion*例程。

如[存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)中所述，存储类驱动程序负责释放为 SRBs 分配的内存，无论是返回后备链表列表还是非分页池。 与任何其他更高级的内核模式驱动程序一样，它们还负责释放它们分配的任何 Irp，如用于拆分传输请求的 IRP，如[存储类驱动程序的 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)中所述。

类驱动程序的*IoCompletion*例程最终负责确保设置了 i/o 状态块并完成了原始 IRP 的设置。 请注意，完成 IRP 可能包括将 SRB 的**ScsiStatus**成员中返回的错误或**SenseInfoBuffer**成员转换为 NTSTATUS 类型值和/或记录错误，如在[调度例程中完成 irp 中](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps-in-dispatch-routines)所述.

当处理请求时出现某些类型的错误时，存储端口驱动程序会冻结其目标逻辑单元（LU）的内部队列，并在请求完成时将 SRB\_状态\_队列\_冻结。 因此，类驱动程序通常有内部例程来更改其设备 i/o 请求的队列状态。 有关详细信息，请参阅[存储类驱动程序的 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)。

如果驱动程序的*BuildRequest*例程请求端口驱动程序为请求返回请求感知信息，则其*IoCompletion*例程要么调用内部*InterpretRequestSense*例程，要么实现相同的功能内联。 有关详细信息，请参阅[存储类驱动程序的 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)。

存储类驱动程序负责重试因目标控制器错误、总线重置或请求超时而失败的请求。 当端口驱动程序返回特定请求，并将其**SrbStatus**设置为指示这种错误时，类驱动程序可以从其*IoCompletion*例程调用*RetryRequest*例程，或从其*InterpretRequestSense*例程。 有关详细信息，请参阅[存储类驱动程序的 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)。

有关*IoCompletion*例程的一般信息，请参阅[完成 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps)。

 

 




