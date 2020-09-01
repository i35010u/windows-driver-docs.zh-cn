---
title: 从调度例程返回状态
description: 从调度例程返回状态
ms.assetid: 76bd651a-344f-4e22-a435-b62fdf2d7ddc
keywords:
- IRP 调度例程 WDK 文件系统，返回状态
- status 值 WDK 文件系统
- 成功状态值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aec5aa4d7d669357c69cf57c3315e216c737e830
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064952"
---
# <a name="returning-status-from-dispatch-routines"></a>从调度例程返回状态


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


除非在完成 IRP 时，未设置完成例程的调度例程应始终返回 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)返回的 NTSTATUS 值。 除非此值处于 \_ "挂起" 状态，否则它必须与完成 irp 的驱动程序设置的 IoStatus 的值匹配** &gt; 。**

将 IRP 设置为可能将 IRP 发布到工作队列的完成例程的调度例程应执行下列操作之一：

-   返回 **IoCallDriver**返回的 NTSTATUS 值。

-   等待完成例程向事件发出信号，并返回 ** &gt; IoStatus**的值。

-   将 IRP 标记为 "挂起"，将其发布到工作队列，并返回 "挂起" 状态 \_ 。

-   如果完成例程可能将 IRP 发送到工作队列，则调度例程必须将 IRP 标记为 "正在挂起" 并返回 "挂起" 状态 \_ 。

这些行为中的哪一个是正确的，甚至可能是这样的：具体取决于特定的操作。 某些操作（例如目录更改通知）无法进行同步;有些（如 oplock）不能成为异步的。

有关从调度例程返回状态的详细信息，请参阅 [调度例程的约束](constraints-on-dispatch-routines.md)。

 

