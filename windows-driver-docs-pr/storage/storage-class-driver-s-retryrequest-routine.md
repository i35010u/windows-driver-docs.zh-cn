---
title: 存储类驱动程序的 RetryRequest 例程
description: 存储类驱动程序的 RetryRequest 例程
ms.assetid: de1eea7d-88db-444c-a9f7-462ad4a5df27
keywords:
- RetryRequest
- 正在重试 WDK 存储
- 错误 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9df89e87b84590d1c4997bf8c04fe458ec0ddce
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187509"
---
# <a name="storage-class-drivers-retryrequest-routine"></a>存储类驱动程序的 RetryRequest 例程


## <span id="ddk_storage_class_drivers_retryrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RETRYREQUEST_ROUTINE_KG"></span>


如果发生了涉及总线上数据传输的设备错误，则基础存储端口驱动程序负责重试请求，其中包括总线奇偶校验错误、选择超时和目标/控制器繁忙错误。 如果重试失败，则存储端口驱动程序将使用适当的错误完成请求并记录 i/o 错误。

存储类驱动程序绝不应尝试重试端口驱动程序由于前面的任何错误而失败的请求。

存储类驱动程序负责重试因设备特定的错误、目标/控制器繁忙、总线重置或请求超时而失败的请求。 通常情况下， *RetryRequest* 例程可以将此类 IRP 重新提交到下一个较低的驱动程序，并将 SRB 置于端口驱动程序的 LU 特定队列的开头。

特别是， *RetryRequest* 例程应该执行以下操作：

1.  确保部分传输请求具有为起始地址和长度设置的正确值。

2.  零： SRB 的 **SrbStatus** 和 **ScsiStatus** 成员。

3.  根据设备的需要，设置 **SrbFlags** 成员。

4.  设置 IRP 中端口驱动程序的 i/o 堆栈位置，如存储类驱动程序的 [调度例程](storage-class-driver-s-dispatch-routines.md) 通过 [存储类驱动程序的 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)所述。

5.  为 IRP 调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，因为在 irp 返回之前，驱动程序的 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程必须释放 SRB。 *IoCompletion*例程可能还需要多次重试请求，或调用驱动程序的*InterpretRequestSense*或*ReleaseQueue*例程。

6.  通过 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将请求传递到下一个较低版本的驱动程序。

 

