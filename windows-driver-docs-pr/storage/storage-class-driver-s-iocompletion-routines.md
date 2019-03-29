---
title: 存储类驱动程序的 IoCompletion 例程
description: 存储类驱动程序的 IoCompletion 例程
ms.assetid: 03cf50be-1b7d-4e5b-8ee5-bbdef860d893
keywords:
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc61ba878b2ef783f0e82eb10ea478a7f72b6130
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576607"
---
# <a name="storage-class-drivers-iocompletion-routines"></a>存储类驱动程序的 IoCompletion 例程


## <span id="ddk_storage_class_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


存储类驱动程序必须具有一个或多个[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，除非该驱动程序同步等待的每个 IRP 发送到端口驱动程序完成后，重试请求，例如在有必要，然后调度中的从 Srb 释放内存或*BuildRequest*例程。 请注意以同步方式处理每个 IRP 会降低类驱动程序的性能。 此外，可能占用系统页面文件必须处理所有的设备的存储类驱动程序以异步方式传输请求，并因此都必须具有*IoCompletion*例程的读/写请求。

如中所述[存储类驱动程序 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)，则存储类驱动程序是负责释放 Srb 为它们分配的内存，是否返回到后备链列表或非分页缓冲池。 像任何其他更高级别的内核模式驱动程序，它们也要负责释放分配它们，如 IRP 来拆分传输请求，如中所述的任何 Irp[存储类驱动程序 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)。

类驱动程序*IoCompletion*例程是最终负责确保设置 I/O 状态块，并完成原始 IRP。 请注意，完成 IRP 可以包含转换错误返回 SRB **ScsiStatus**成员或**SenseInfoBuffer**到 NTSTATUS 类型值和/或日志记录错误，如中所述的成员[完成调度例程中的 Irp](https://msdn.microsoft.com/library/windows/hardware/ff542019)。

在某些类型的错误发生在处理请求，存储端口驱动程序目标逻辑单元 (LU) 将冻结其内部队列并设置 SRB\_状态\_队列\_上请求完成的冻结。 因此，类驱动程序通常具有内部例程，从而更改其设备 I/O 请求的队列的状态。 有关详细信息，请参阅[存储类驱动程序 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)。

如果驱动程序的*BuildRequest*例程请求端口驱动程序返回的请求，请求检测信息及其*IoCompletion*日常操作会调用内部*InterpretRequestSense*例程或实现相同功能内联。 有关详细信息，请参阅[存储类驱动程序 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)。

存储类驱动程序负责重试由于目标控制器错误、 总线重置或请求超时而失败的请求。 当端口驱动程序返回的特定请求其**SrbStatus**设置，以指示此类错误，可以调用的类驱动程序*RetryRequest*例程从其*IoCompletion*例程或可能是从其*InterpretRequestSense*例程。 有关详细信息，请参阅[存储类驱动程序 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)。

有关常规信息*IoCompletion*例程，请参阅[完成 Irp](https://msdn.microsoft.com/library/windows/hardware/ff542018)。

 

 




