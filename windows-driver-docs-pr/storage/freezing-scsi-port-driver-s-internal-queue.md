---
title: 冻结 SCSI 端口驱动程序的内部队列
description: 冻结 SCSI 端口驱动程序的内部队列
ms.assetid: 8e93b7d4-8429-43ec-a439-75cfeaa95887
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d5ad502d05dd12a0877fa9332cb3cc0b64fbe2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545331"
---
# <a name="freezing-scsi-port-drivers-internal-queue"></a>冻结 SCSI 端口驱动程序的内部队列


## <span id="ddk_freezing_scsi_port_drivers_internal_queue_kg"></span><span id="DDK_FREEZING_SCSI_PORT_DRIVERS_INTERNAL_QUEUE_KG"></span>


SCSI 端口驱动程序的错误条件时，需要从类驱动程序的约束性仲裁冻结其内部队列。 冻结队列允许 SCSI 端口报告错误条件的类驱动程序，并使类驱动程序可以在之后继续保留在队列中的请求处理分析错误。 例如，如果更改媒体的排队的请求可能需要取消，但约束性仲裁类驱动程序是必需的。 仅在类驱动程序具有足够的上下文信息以确定是否删除某些类型的媒体会影响特定的请求。

如果存储类驱动程序 ORs **SrbFlags**针对给定请求与 SRB\_标志\_否\_队列\_冻结、 SCSI 端口不会冻结问题，由于其队列特定请求。 否则，SCSI 端口冻结任何以下情况下的其队列：

-   设备会拒绝请求，并返回状态为 SCSISTAT\_检查\_条件或 SCSISTAT\_命令\_已终止

-   请求超时

-   设备正在执行请求时发生总线重置

-   由总线邮件命令如 SCSIMESS 终止请求\_中止

SCSI 端口指示其队列通过返回请求导致与 SRB 冻结冻结\_状态\_队列\_中设置的冻结标志**SrbStatus** SRB 的成员。 SCSI 端口将任何新请求中的类驱动程序插入到队列，但只要队列已被冻结 SCSI 端口将不会转发到以外自动感知和 power 请求设备的任何请求。

如果 SRB\_标志\_绕过\_冻结\_中设置队列标志**SrbFlags**成员的请求，SCSI 端口会绕过冻结的队列并立即执行该请求。 在其中的任何后续请求**SrbFlags**是或运算使用 SRB\_标志\_绕过\_冻结\_队列将导致 SCSI 端口以刷新的队列。

更高级别的驱动程序可以强制 SCSI 端口取消其队列使用 SRB\_函数\_释放\_队列发布队列请求。 SRB\_函数\_刷新\_队列还取消队列冻结后取消所有排队的请求。

 

 




