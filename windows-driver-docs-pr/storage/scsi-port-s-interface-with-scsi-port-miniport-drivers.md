---
title: SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口
description: SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口
ms.assetid: e6bd9861-5b89-40cc-92ab-0d23f18ba805
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7397064af53122863dc652116ef793160370c47e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378173"
---
# <a name="scsi-ports-interface-with-scsi-port-miniport-drivers"></a>SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口


## <span id="ddk_scsi_port_s_interface_with_scsi_port_miniport_drivers_kg"></span><span id="DDK_SCSI_PORT_S_INTERFACE_WITH_SCSI_PORT_MINIPORT_DRIVERS_KG"></span>


SCSI 端口驱动程序和 SCSI 端口微型端口驱动程序之间的通信发生通过 SCSI 请求块 (Srb) 和微型端口驱动程序回调例程。 SCSI 端口微型端口驱动程序回调例程的详细讨论，请参阅[SCSI 微型端口驱动程序](scsi-miniport-drivers.md)。

有关概述，以及各个 SRB 函数、 SRB 标志和 SRB 状态值的定义，请参阅[ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393)。

有关如何微型端口驱动程序必须应对每个 SRB 函数的讨论，请参阅[SCSI 微型端口驱动程序 HwScsiStartIo 例程](scsi-miniport-driver-s-hwscsistartio-routine.md)。

SCSI 端口将转发 Srb 到 SCSI 端口微型端口驱动程序同步，除非该适配器支持有标记的队列。 支持有标记的队列的主机总线适配器可以在内部对请求进行排队，并指示由标记 SCSI 端口分配到每个请求的顺序处理它们。 [ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393) (SRB) 结构包含两个成员 SCSI 端口驱动程序用来指定 Srb 主机适配器的内部队列中的排序方式:**QueuedTag**并**QueueAction**。 SCSI 端口分配计数，或 *"标记"* 值，为**QueuedTag**指示适配器应在其中处理的数据包的顺序的每个 SRB 的成员。 标记值还允许 SCSI 端口来跟踪哪些 Srb 已成功完成，哪些 Srb 已超时。

**QueueAction**成员分配以下值之一：

SRB\_简单\_标记\_请求

SRB\_HEAD\_OF\_队列\_标记\_请求

SRB\_ORDERED\_队列\_标记\_请求

有关这些值的说明，请参阅 SCSI 2 规范。

 

 




