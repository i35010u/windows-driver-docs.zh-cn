---
title: 在 UMDF 中重复使用 Framework 请求对象
description: 在 UMDF 中重复使用 Framework 请求对象
ms.assetid: 804efc94-a7df-4ebd-a42e-82d1c5376e19
keywords:
- I/o 请求 WDK UMDF，重复使用对象
- 请求处理 WDK UMDF，并重复使用 i/o 请求对象
- 用户模式驱动程序框架 WDK，重用 i/o 请求对象
- UMDF WDK，重复使用 i/o 请求对象
- 用户模式驱动程序 WDK UMDF，重用 i/o 请求对象
- 重复使用 i/o 请求对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9785cf2179b9595b4a1a26f6d46d1fb3d85a5f59
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210865"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>在 UMDF 中重复使用 Framework 请求对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

若要改善驱动程序性能，创建并向 i/o 目标发送很多几乎相同的异步请求的基于框架的驱动程序可以重复使用请求对象，而不是为每个请求创建新的请求对象。 请求完成后，驱动程序可以重复使用请求对象。

如果驱动程序已通过调用[**IWDFDevice：： CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)创建了 request 对象，则它可以通过调用[**IWDFIoRequest2：：重用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)来重复使用该请求。 驱动程序还可以重用从其 i/o 队列中的框架收到的请求对象。

如果驱动程序为其重用的请求对象提供[**IRequestCallbackRequestCompletion：： OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)回调函数，则驱动程序必须在调用[**重新使用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)后调用[**IWDFIoRequest：： SetCompletionCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback) 。

 

 





