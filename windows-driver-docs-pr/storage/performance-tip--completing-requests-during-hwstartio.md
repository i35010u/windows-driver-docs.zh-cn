---
title: 性能提示完成请求期间 HwStartIo
description: 性能提示完成请求期间 HwStartIo
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 476354ba5f39792cab08f072a54a2d779b25272c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358476"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>性能提示：在 HwStartIo 期间完成请求


通过完成未完成的 I/O 请求已准备好进行中的完成其[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)例程，微型端口可以花费更少的时间设备 IRQL (DIRQL)，从而提高系统的响应能力，并此外可以利用新的 Storport 优化，进一步提高系统的响应能力和 I/O 吞吐量。 要点是尝试时间尽可能中断处理程序。 若要充分利用新的 Storport 优化微型端口：

-   必须启用通过 DPC 重定向[ **StorPortInitializePerfOpts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitializeperfopts)

-   必须使用[ **StorPortNotification (NotificationType = RequestComplete)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)中时，在其[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)例程，以通知Storport 的已完成的 I/O 请求

-   应指示其旨在通过设置存储帐户是否进行完成期间 StartIo\_PERF\_优化\_有关\_完成\_在\_对其调用中的STARTIO标志[ **StorPortInitializePerfOpts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitializeperfopts)例程

-   必须确定应应用优化前存在的工作负荷 （例如，请求大小和吞吐量） 的特征。

中时，其[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)例程，微型端口应检查已完成请求的启动请求的 I/O 操作后。

 

 




