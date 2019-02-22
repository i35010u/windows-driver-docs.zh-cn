---
title: 重复使用在 UMDF Framework 请求对象
description: 重复使用在 UMDF Framework 请求对象
ms.assetid: 804efc94-a7df-4ebd-a42e-82d1c5376e19
keywords:
- I/O 请求 WDK UMDF，重用对象
- 请求处理 WDK UMDF，重复使用 I/O 请求对象
- 用户模式驱动程序框架 WDK，重复使用 I/O 请求对象
- UMDF WDK，重复使用 I/O 请求对象
- 用户模式驱动程序 WDK UMDF，重复使用 I/O 请求对象
- 重复使用的 I/O 请求对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19ffa2641991b83a35abade8ec15b182f206500e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546317"
---
# <a name="reusing-framework-request-objects-in-umdf"></a>重复使用在 UMDF Framework 请求对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

若要提高驱动程序性能，基于框架的驱动程序的创建和发送许多几乎完全相同的异步请求到 I/O 的目标可以重复使用的请求而不是创建每个请求一个新的请求对象的对象。 请求完成后，驱动程序可以重复使用一个请求对象。

如果驱动程序已通过调用创建一个请求对象[ **IWDFDevice::CreateRequest**](https://msdn.microsoft.com/library/windows/hardware/ff557021)，它可以通过调用重用请求[ **IWDFIoRequest2::Reuse**](https://msdn.microsoft.com/library/windows/hardware/ff559048). 驱动程序也可以重复使用它从其 I/O 队列中的框架接收的请求对象。

如果您的驱动程序提供了[ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)它重用一个请求对象的回调函数，该驱动程序必须调用[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)它调用后[**重用**](https://msdn.microsoft.com/library/windows/hardware/ff559048)。

 

 





