---
title: 将存储请求排队
description: 将存储请求排队
ms.assetid: 077f7e4f-feb5-4a2e-b22b-b1d8d6871987
keywords:
- 外围设备 WDK 存储，排队的请求
- 存储外围设备 WDK，排队的请求
- 排队的请求 WDK 存储
- 队列 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcde1f1ff09d4e2e4681e402a996f513a3bd00e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366456"
---
# <a name="queuing-storage-requests"></a>将存储请求排队


## <span id="ddk_queueing_storage_requests_kg"></span><span id="DDK_QUEUEING_STORAGE_REQUESTS_KG"></span>


虽然可以为 Irp 设置内部队列的存储类驱动程序，它是很少必须这样做，可能会降低，驱动程序的性能由于存储端口驱动程序已维护驱动程序创建的特定于 LU 的设备队列有关 Irp。 特定 HBA 是否支持多个未完成的命令 （例如，SCSI 有标记的队列），或存储类驱动程序可以将每个请求发送到其设备，如每个 IRP 传入和依赖于系统提供的端口驱动程序来处理 HBA 排入队列请求能迅速。

发生某些 SCSI 错误时，系统端口驱动程序会冻结相应的特定于 LU 的队列，并通知的类驱动程序。 有关处理错误和释放冻结的请求队列的详细信息，请参阅：

[存储类驱动程序 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)

[存储类驱动程序 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)

[存储类驱动程序 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)

如果 HBA 支持命令排队，返回的存储中所示\_适配器\_描述符数据的类驱动程序设置 SRB\_标志\_队列\_启用和使用**QueueAction** Srb 它将创建来控制其请求会排入队列的成员。

 

 




