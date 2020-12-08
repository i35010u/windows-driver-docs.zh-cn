---
title: 重复使用框架请求对象
description: 重复使用框架请求对象
keywords:
- 请求处理 WDK KMDF，重复使用请求对象
- 请求对象 WDK KMDF，重复使用
- 重复使用请求对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4758deffe962035c491bfdd895d2358b9156de2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803443"
---
# <a name="reusing-framework-request-objects"></a>重复使用框架请求对象





若要提高性能，创建并向 i/o 目标发送很多几乎相同的异步请求的基于框架的驱动程序可以重复使用请求对象，而不是为每个请求创建新的请求对象。 请求完成后，驱动程序可以重复使用请求对象。

如果驱动程序已通过调用 [**WdfRequestCreate**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate) 或 [**WdfRequestCreateFromIrp**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)创建了 request 对象，则它可以通过调用 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)重复使用该请求。 驱动程序还可以重用从其 i/o 队列中的框架收到的请求对象，但它不能更改收到的请求对象包含的 IRP。

如果要小心避免导致 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)中所述的返回值不成功的情况，驱动程序可以从 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数中调用 **WdfRequestReuse** 。  (*CompletionRoutine* 回调函数具有 VOID 返回值，因此无法报告错误。 ) 

如果驱动程序为其重用的请求对象提供 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，则驱动程序必须在调用 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)后调用 [**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine) 。

 

