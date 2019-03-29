---
title: 完成 I/O 请求在 UMDF
description: 完成 I/O 请求在 UMDF
ms.assetid: 3f8c7030-7c5d-4f65-8001-592af0b1d2de
keywords:
- I/O 请求 WDK UMDF，完成
- 请求处理 WDK UMDF，完成请求
- 完成 I/O 请求 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de08ba935b045cc2c6e16f8ff8bf076374afdde1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568602"
---
# <a name="completing-io-requests-in-umdf"></a>完成 I/O 请求在 UMDF


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

每个 I/O 请求最终必须通过 UMDF 驱动程序。 若要完成请求，该驱动程序必须调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)方法。 该驱动程序完成请求，它表示以下方案之一：

-   请求的 I/O 操作成功完成。

-   请求的 I/O 操作启动，但它完成之前失败。

-   请求的 I/O 操作不受支持，或在其已接收到，因此不能与设备通信的时间无效。

-   请求的 I/O 操作已[取消](canceling-i-o-requests.md)。

驱动程序调用[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)方法传递的请求操作有关的其他信息。 例如，对于读取操作，该驱动程序应提供读取的字节数。

若要完成的 I/O 请求，该驱动程序必须通过相应的完成状态设置为*CompletionStatus*调用中的参数[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)。 该驱动程序使用 HRESULT 代码通信已完成请求的状态。

[UMDF 驱动程序主机进程](umdf-driver-host-process.md)转换为 HRESULT 代码 NTSTATUS 代码已完成的请求传递到该发送程序 (Wudfrd.sys) 之前。 该发送程序将 NTSTATUS 代码传递给操作系统。 它提供了将结果发送到调用应用程序之前，操作系统会将 NTSTATUS 代码转换为 Microsoft Win32 错误代码。

若要确保可以正确地转换您的驱动程序的错误代码，应通过以下方法之一创建错误代码：

-   使用从 Winerror.h 错误代码，并应用相应的 HRESULT\_FROM\_WIN32 宏。

-   使用从 Ntstatus.h 错误代码，并应用相应的 HRESULT\_FROM\_NT 宏。

有关这些宏的详细信息，请参阅 Microsoft Windows SDK 文档。

下面的代码示例演示如何完成适当的错误代码的请求：

```cpp
VOID
STDMETHODCALLTYPE
CMyQueue::OnWrite(
    __in IWDFIoQueue *pWdfQueue,
    __in IWDFIoRequest *pWdfRequest,
    __in SIZE_T BytesToWrite
    )
{
            -------------------- 
    if( BytesToWrite > MAX_WRITE_LENGTH ) {
        pWdfRequest->CompleteWithInformation(HRESULT_FROM_WIN32(ERROR_MORE_DATA), 0);
        return;
    }
            ---------------------
}
```

当驱动程序成功完成请求时，它将返回 S\_确定，这是 HRESULT 值。 因为 S\_确定相当于否\_Winerror.h 和状态中的错误\_宏，则不需要的转换 Ntstatus.h 中发现了成功。

如果[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)启用了 reflector，它标识无效的状态代码并将导致系统出现 bugcheck。

**请注意**  驱动程序验证工具适用于 Windows XP 不正确会导致系统出现 bugcheck 的 Win32 错误代码的值超过十进制 1024 (1024 L)。 如果您的驱动程序在 Windows XP 上运行，请注意此问题的如果为该发送程序启用驱动程序验证程序。

 

如果驱动程序以前发送请求到较低级别驱动程序，该驱动程序在较低级驱动程序完成请求时需要通知。 若要注册通知，该驱动程序调用[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)方法来注册时，框架调用的方法的接口的较低级驱动程序完成请求。 该驱动程序实现[ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)回调函数以执行完成请求所需的操作。

驱动程序不会完成它已通过调用创建的 I/O 请求[ **IWDFDevice::CreateRequest**](https://msdn.microsoft.com/library/windows/hardware/ff557021)。 相反，该驱动程序必须调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210) I/O 目标完成请求后通常删除请求对象。

例如，驱动程序可能会收到读取或写入请求的数据大于驱动程序的 I/O 目标可以处理一次。 该驱动程序必须将数据划分为多个较小请求，并将这些较小的请求发送到一个或多个 I/O 目标。 处理这种情况的方法包括：

-   调用[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)来创建一个额外的请求对象表示的较小的请求。

    该驱动程序可以向 I/O 目标以同步方式发送此请求。 较小请求[ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)回调函数可以调用[ **IWDFIoRequest2::Reuse** ](https://msdn.microsoft.com/library/windows/hardware/ff559048)，以便该驱动程序可以重新使用该请求并再次将其发送到 I/O 目标。 I/O 目标完成的较小的请求，最后一个后**OnCompletion**回调函数可以调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)删除驱动程序创建请求对象，该驱动程序可以调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)完成原始请求。

-   调用[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)来创建多个额外的请求对象，表示较小的请求。

    驱动程序的 I/O 目标可以以异步方式处理这些多个较小的请求。 该驱动程序可以注册[ **OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)为每个较小的请求的回调函数。 每次**OnCompletion**调用回调函数，它可以调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)删除驱动程序创建请求对象。 该驱动程序 I/O 目标完成所有较小的请求后，可以调用[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)完成原始请求。

### <a name="obtaining-completion-information"></a>获取完成信息

若要获取有关另一个驱动程序已完成的 I/O 请求的信息，请基于 UMDF 驱动程序可以：

-   使用[ **IWDFRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff560292)接口，以获得的 I/O 请求的完成状态和其他信息。

-   使用[ **IWDFIoRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff559055)接口，以获得的 I/O 请求的内存缓冲区。

-   使用[ **IWDFUsbRequestCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff560346)接口来获取内存缓冲区和其他信息与已发送到的 USB 目标管道对象的请求。

此外，可以使用基于 UMDF 驱动程序[ **IWDFIoRequest2::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559013)方法来获取的 I/O 请求的当前状态之前或之后完成请求。

 

 





