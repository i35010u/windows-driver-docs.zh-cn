---
title: 从调度例程返回状态
description: 从调度例程返回状态
ms.assetid: 76bd651a-344f-4e22-a435-b62fdf2d7ddc
keywords:
- IRP 调度例程 WDK 文件系统中，返回状态
- 状态值 WDK 文件系统
- 成功状态的值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea021e58d61e949c1a44645084d8f1c5a07e1ee9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385937"
---
# <a name="returning-status-from-dispatch-routines"></a>从调度例程返回状态


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


但不会设置完成例程的调度例程完成后 IRP，应始终返回返回的 NTSTATUS 值[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。 除非此值为状态\_挂起状态，它必须匹配的值**Irp-&gt;IoStatus.Status**完成 IRP 驱动程序设置。

设置可能会发布到工作队列 IRP 完成例程的调度例程应执行以下操作：

-   返回由返回的 NTSTATUS 值**IoCallDriver**。

-   等待完成例程来指示事件，并返回的值**Irp-&gt;IoStatus.Status**。

-   将标记挂起的 IRP，将其发布到工作队列，并返回状态\_PENDING。

-   如果完成例程可能会发布到工作队列 IRP，必须将挂起的 IRP 标记并返回状态的调度例程\_PENDING。

其中这些行为是正确的或甚至、 取决于特定操作。 某些操作，例如目录更改通知，无法进行同步的而一些，如 oplock，不能成为异步。

有关从调度例程返回状态的详细信息，请参阅[调度例程的约束](constraints-on-dispatch-routines.md)。

 

 




