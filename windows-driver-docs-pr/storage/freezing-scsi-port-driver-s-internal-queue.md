---
title: 冻结 SCSI 端口驱动程序的内部队列
description: 冻结 SCSI 端口驱动程序的内部队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d42fc81528863b7eb24fa1d368231a9be3da3336
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835299"
---
# <a name="freezing-scsi-port-drivers-internal-queue"></a>冻结 SCSI 端口驱动程序的内部队列


## <span id="ddk_freezing_scsi_port_drivers_internal_queue_kg"></span><span id="DDK_FREEZING_SCSI_PORT_DRIVERS_INTERNAL_QUEUE_KG"></span>


每当出现需要类驱动程序的仲裁的错误条件时，SCSI 端口驱动程序就会冻结其内部队列。 冻结队列允许 SCSI 端口向类驱动程序报告错误条件，并为类驱动程序在继续处理保留在队列中的请求之前有机会分析错误。 例如，如果更改了媒体，则可能需要取消排队的请求，但需要类驱动程序的仲裁。 仅类驱动程序具有足够的上下文信息，以确定是否删除特定类型的媒体会影响特定的请求。

如果存储类驱动程序为给定请求 Or **SrbFlags** ，而 SRB \_ 标志 \_ 没有 \_ 队列 \_ 冻结，则 SCSI 端口不会因特定请求出现问题而冻结其队列。 否则，SCSI 端口将在以下任何条件下冻结其队列：

-   设备未通过请求并返回状态 SCSISTAT \_ 检查 \_ 条件或 SCSISTAT \_ 命令已 \_ 终止

-   请求超时

-   在设备执行请求时发生总线重置

-   请求由总线消息命令终止，如 SCSIMESS \_ 中止

SCSI 端口通过返回在 \_ \_ SRB 的 \_ **SrbStatus** 成员中设置了 SRB 状态队列冻结标志的请求来冻结其队列。导致 SCSI 端口会将类驱动程序发出的所有新请求插入到队列中，但只要队列被冻结，SCSI 端口就不会将任何请求转发到自动探测和电源请求以外的其他设备。

如果 \_ \_ \_ \_ 在请求的 **SRBFLAGS** 成员中设置了 SRB 标志 "跳过队列" 标志，则 SCSI 端口会绕过冻结队列并立即执行请求。 任何后续请求（其中 **SrbFlags** 为运算，而 SRB \_ 标志 \_ 绕过 \_ 冻结队列） \_ 将导致 SCSI 端口刷新队列。

更高级别的驱动程序可以使用 SRB \_ 函数 \_ release \_ queue release QUEUE 请求强制 SCSI 端口解除冻结其队列。 SRB \_ 函数 \_ 刷新 \_ 队列还会在取消所有已排队的请求后 unfreezes 队列。

 

 




