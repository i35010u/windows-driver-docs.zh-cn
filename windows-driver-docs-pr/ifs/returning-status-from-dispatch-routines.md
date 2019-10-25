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
ms.openlocfilehash: 09b464f79b79c54821ef491ec004670dc68bc075
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840987"
---
# <a name="returning-status-from-dispatch-routines"></a>从调度例程返回状态


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


除非在完成 IRP 时，未设置完成例程的调度例程应始终返回[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)返回的 NTSTATUS 值。 除非此值为 "状态"\_"挂起"，否则它必须与完成 IRP 的驱动程序设置的**irp&gt;IoStatus**的值匹配。

将 IRP 设置为可能将 IRP 发布到工作队列的完成例程的调度例程应执行下列操作之一：

-   返回**IoCallDriver**返回的 NTSTATUS 值。

-   等待完成例程向事件发出信号，并返回**Irp&gt;IoStatus**的值。

-   将 IRP 标记为 "挂起"，将其发布到工作队列，并返回状态\_"挂起"。

-   如果完成例程可能将 IRP 发送到工作队列，则调度例程必须将 IRP 标记为 "正在挂起" 并返回状态\_"挂起"。

这些行为中的哪一个是正确的，甚至可能是这样的：具体取决于特定的操作。 某些操作（例如目录更改通知）无法进行同步;有些（如 oplock）不能成为异步的。

有关从调度例程返回状态的详细信息，请参阅[调度例程的约束](constraints-on-dispatch-routines.md)。

 

 




