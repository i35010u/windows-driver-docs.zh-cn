---
title: 在 UMDF 中重复使用 Framework 请求对象
description: 在 UMDF 中重复使用 Framework 请求对象
keywords:
- I/o 请求 WDK UMDF，重复使用对象
- 请求处理 WDK UMDF，并重复使用 i/o 请求对象
- User-Mode Driver Framework WDK，重用 i/o 请求对象
- UMDF WDK，重复使用 i/o 请求对象
- 用户模式驱动程序 WDK UMDF，重用 i/o 请求对象
- 重复使用 i/o 请求对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dd35032f3ef31126ed6b0e63cbea3d935b753cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783683"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>在 UMDF 中重复使用 Framework 请求对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

若要改善驱动程序性能，创建并向 i/o 目标发送很多几乎相同的异步请求的基于框架的驱动程序可以重复使用请求对象，而不是为每个请求创建新的请求对象。 请求完成后，驱动程序可以重复使用请求对象。

如果驱动程序已通过调用 [**IWDFDevice：： CreateRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)创建了 request 对象，则它可以通过调用 [**IWDFIoRequest2：：重用**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)来重复使用该请求。 驱动程序还可以重用从其 i/o 队列中的框架收到的请求对象。

如果驱动程序为其重用的请求对象提供 [**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)回调函数，则驱动程序必须在调用 [**重新使用**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)后调用 [**IWDFIoRequest：： SetCompletionCallback**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback) 。

 

