---
title: 刷新端口驱动程序的内部队列
description: 刷新端口驱动程序的内部队列
ms.assetid: b0e6762e-0380-4ff5-aac7-36bdb5a60aa7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8e0d9914f9f54bb48e2a60e20cba8ede9bd24a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355891"
---
# <a name="flushing-port-drivers-internal-queue"></a>刷新端口驱动程序的内部队列


## <span id="ddk_flushing_port_driver_s_internal_queue_kg"></span><span id="DDK_FLUSHING_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


SCSI 端口驱动程序支持允许更高级别的驱动程序将在内部，缓存数据刷新的设备和适配器缓存的刷新请求。 若要维护数据完整性之前在系统关闭的情况下, 应刷新所有内部缓存。 在收到的刷新请求时 SCSI 端口刷新，其自身内部队列取消排队的所有请求。

更高级别的驱动程序可以通过将刷新主机适配器的缓存和 SCSI 端口的内部队列发送类型 SRB SRB\_函数\_刷新\_SCSI 端口驱动程序的队列。 SCSI 端口刷新主机适配器缓存，然后完成所有请求使用其内部队列中的收到此 SRB 时，其**SrbStatus**成员设置为 SRB\_状态\_请求\_刷新。 如果 SCSI Port 的队列被冻结，SRB\_函数\_刷新\_队列具有副作用的解除冻结队列。

有关如何存储微型端口驱动程序处理冲洗请求的讨论，请参阅[处理 SRB\_函数\_刷新和 SRB\_函数\_关闭](handling-srb-function-flush-and-srb-function-shutdown.md)。

 

 




