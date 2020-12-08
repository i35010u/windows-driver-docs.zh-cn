---
title: 将存储请求排队
description: 将存储请求排队
keywords:
- 外围设备 WDK 存储，排队请求
- 存储外围设备 WDK，排队的请求
- 排队请求 WDK 存储
- 队列 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d459bb7293379a7100b03410e0b4c5b78a23639
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832083"
---
# <a name="queuing-storage-requests"></a>将存储请求排队


## <span id="ddk_queueing_storage_requests_kg"></span><span id="DDK_QUEUEING_STORAGE_REQUESTS_KG"></span>


尽管存储类驱动程序可以为 Irp 设置内部队列，但很少需要这样做，并且很可能会降低驱动程序的性能，因为存储端口驱动程序已经为 Irp 维护了驱动程序创建的、LU 特定的设备队列。 无论某个 HBA 是否支持多个未处理的命令 (例如，SCSI 标记队列) ，存储类驱动程序在每个 IRP 进入并依赖系统提供的端口驱动程序或 HBA 处理排队请求迅速时，可以将每个请求发送到其设备。

发生某些 SCSI 错误时，系统端口驱动程序会冻结适当的特定于 LU 的队列，并通知类驱动程序。 有关处理错误和释放冻结请求队列的详细信息，请参阅以下内容：

[存储类驱动程序的 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)

[存储类驱动程序的 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)

[存储类驱动程序的 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)

如果 HBA 支持命令队列（如返回的存储 \_ 适配器描述符数据所示） \_ ，类驱动程序将设置 SRB \_ 标志队列， \_ \_ 并使用它创建的 SRBs 的 **QueueAction** 成员来控制其请求的排队方式。

 

 




