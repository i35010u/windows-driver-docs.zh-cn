---
title: 重复使用框架请求对象
description: 重复使用框架请求对象
ms.assetid: 9e3090a9-62d0-48b3-9f3b-7171dc6d2766
keywords:
- 请求处理 WDK KMDF，重复使用请求对象
- 请求对象 WDK KMDF，重复使用
- 重复使用请求对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498cf85da837e32a0cc752a1b70f5522bf6e2fac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842209"
---
# <a name="reusing-framework-request-objects"></a>重复使用框架请求对象





若要提高性能，创建并向 i/o 目标发送很多几乎相同的异步请求的基于框架的驱动程序可以重复使用请求对象，而不是为每个请求创建新的请求对象。 请求完成后，驱动程序可以重复使用请求对象。

如果驱动程序已通过调用[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)或[**WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)创建了 request 对象，则它可以通过调用[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)重复使用该请求。 驱动程序还可以重用从其 i/o 队列中的框架收到的请求对象，但它不能更改收到的请求对象包含的 IRP。

如果要小心避免导致[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)中所述的返回值不成功的情况，驱动程序可以从[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数中调用**WdfRequestReuse** 。 （ *CompletionRoutine*回调函数具有 VOID 返回值，因此无法报告错误。）

如果驱动程序为其重用的请求对象提供[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数，则驱动程序必须在调用[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)后调用[**WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine) 。

 

 





