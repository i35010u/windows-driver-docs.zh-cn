---
title: 存储类驱动程序的 RetryRequest 例程
description: 存储类驱动程序的 RetryRequest 例程
ms.assetid: de1eea7d-88db-444c-a9f7-462ad4a5df27
keywords:
- RetryRequest
- 正在重试请求 WDK 存储
- 错误 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd56a8ef9820c25c7ffd27add77964b84cdabe4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379091"
---
# <a name="storage-class-drivers-retryrequest-routine"></a>存储类驱动程序的 RetryRequest 例程


## <span id="ddk_storage_class_drivers_retryrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RETRYREQUEST_ROUTINE_KG"></span>


基础存储端口驱动程序负责涉及到总线，包括总线奇偶校验错误、 选择超时值和目标/控制器忙错误上的数据的传输设备错误发生的情况下重试请求。 如果重试尝试都失败，存储端口驱动程序完成请求因相应的错误和日志 I/O 错误。

存储类驱动程序应永远不会尝试重试端口驱动程序已由于上面的错误的任何失败的请求。

存储类驱动程序负责因特定于设备的错误，以外目标/控制器-忙，总线重置的目标/控制器错误而失败或请求超时值的重试请求。 一般情况下， *RetryRequest*例程可以重新提交此类 IRP 到下一步低驱动程序并直接 SRB 将放在端口驱动程序的特定于 LU 的队列的开头处。

具体而言， *RetryRequest*例程应执行以下操作：

1.  确保分部传输请求已正确设置的起始地址和长度的值。

2.  零**SrbStatus**并**ScsiStatus** SRB 的成员。

3.  设置**SrbFlags**成员，根据需要为该设备。

4.  设置中 IRP 如前面所述的端口驱动程序的 I/O 堆栈位置[存储类驱动程序调度例程](storage-class-driver-s-dispatch-routines.md)通过[存储类驱动程序 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)。

5.  调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)的 IRP，因为在驱动程序[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程必须释放之前 IRP SRB返回。 *IoCompletion*不止一次重试请求或调用的驱动程序，可能还需要例程*InterpretRequestSense*或*ReleaseQueue*例程。

6.  将请求传递到下一步低驱动程序和[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

 

 




