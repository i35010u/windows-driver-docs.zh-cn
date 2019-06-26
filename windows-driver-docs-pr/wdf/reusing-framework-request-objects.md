---
title: 重复使用框架请求对象
description: 重复使用框架请求对象
ms.assetid: 9e3090a9-62d0-48b3-9f3b-7171dc6d2766
keywords:
- 请求处理 WDK KMDF、 重复使用的请求对象
- 请求对象 WDK KMDF，重复使用
- 重复使用请求对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55daabf712c2bdb2249cc8c2195cf39088f176ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376247"
---
# <a name="reusing-framework-request-objects"></a>重复使用框架请求对象





若要提高性能，基于框架的驱动程序的创建和发送大量 I/O 目标几乎完全相同的异步请求可以重复使用的请求而不是创建每个请求一个新的请求对象的对象。 请求完成后，驱动程序可以重复使用一个请求对象。

如果驱动程序已通过调用创建一个请求对象[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)或[ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)，它可以重复使用该请求通过调用[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)。 驱动程序也可以重复使用它从其 I/O 队列中的框架接收的请求对象，但它不能更改收到的请求对象包含 IRP。

如果你非常小心地避免会导致不成功的返回值中所述的情况下[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)，您的驱动程序可以调用**WdfRequestReuse**中[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)回调函数。 ( *CompletionRoutine*回调函数有一个空返回值，因此不能报告错误。)

如果您的驱动程序提供了[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)它重用一个请求对象的回调函数，该驱动程序必须调用[ **WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)后调用[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)。

 

 





