---
title: 在 UMDF 中完成 i/o 请求
description: 在 UMDF 中完成 i/o 请求
ms.assetid: 3f8c7030-7c5d-4f65-8001-592af0b1d2de
keywords:
- I/o 请求 WDK UMDF，完成
- 请求处理 WDK UMDF，完成请求
- 完成 i/o 请求 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3eed1286802e005d9d753006d691ede08e40eb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185319"
---
# <a name="completing-io-requests-in-umdf"></a>在 UMDF 中完成 i/o 请求


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

每个 i/o 请求最终必须由 UMDF 驱动程序完成。 若要完成请求，驱动程序必须调用 [**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 或 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation) 方法。 当驱动程序完成请求时，它表示下列方案之一：

-   请求的 i/o 操作已成功完成。

-   请求的 i/o 操作已启动，但在完成之前失败。

-   请求的 i/o 操作在收到时不受支持或无效，因此无法与设备通信。

-   已 [取消](canceling-i-o-requests.md)请求的 i/o 操作。

驱动程序调用 [**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation) 方法以传递有关请求操作的其他信息。 例如，对于读取操作，驱动程序应提供读取的字节数。

若要完成 i/o 请求，驱动程序必须在对[**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)或[**IWDFIoRequest：： CompleteWithInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)的调用中，将相应的完成状态传递到*CompletionStatus*参数。 驱动程序使用 HRESULT 代码来传达完成的请求的状态。

在将已完成的请求传递到反射器 ( # A0) 之前， [UMDF 驱动程序主机进程](umdf-driver-host-process.md) 将 HRESULT 代码转换为 NTSTATUS 代码。 反射器将 NTSTATUS 代码传递到操作系统。 在向调用应用程序显示结果之前，操作系统会将 NTSTATUS 代码转换为 Microsoft Win32 错误代码。

若要确保驱动程序的错误代码可以正确转换，应通过以下任一方法来创建错误代码：

-   使用 Winerror.h 中的错误代码，并 \_ 从 WIN32 宏应用 HRESULT \_ 。

-   使用 Ntstatus 中的错误代码，并 \_ 从 NT 宏应用 HRESULT \_ 。

有关这些宏的详细信息，请参阅 Microsoft Windows SDK 文档。

下面的示例代码演示如何使用适当的错误代码来完成请求：

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

当驱动程序成功完成请求时，它将返回 \_ "OK"，这是一个 HRESULT 值。 由于 S \_ OK 等效于 winerror.h 中的无 \_ 错误和 \_ NTSTATUS 中的状态 SUCCESS，因此不需要转换宏。

如果为反射器启用了 [驱动程序验证程序](../devtest/driver-verifier.md) ，则它将标识无效的状态代码并导致系统错误检查。

**注意**   适用于 Windows XP 的驱动程序验证程序不正确导致 Win32 错误代码的系统错误检查，其值超过小数点 1024 (1024L) 。 如果你的驱动程序在 Windows XP 上运行，请注意此问题（如果你为反射器启用了驱动程序验证程序）。

 

如果驱动程序先前已将请求发送到较低级别的驱动程序，则驱动程序在低级驱动程序完成请求时需要通知。 若要注册通知，驱动程序将调用 [**IWDFIoRequest：： SetCompletionCallback**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback) 方法，以便为框架在较低级别的驱动程序完成请求时所调用的方法注册接口。 驱动程序实现 [**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) 回调函数以执行完成请求所需的操作。

驱动程序不会完成通过调用 [**IWDFDevice：： CreateRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)创建的 i/o 请求。 相反，驱动程序必须调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 删除请求对象，通常是在 i/o 目标完成请求后。

例如，对于大于驱动程序的 i/o 目标可以一次处理的数据量，驱动程序可能会收到读取或写入请求。 驱动程序必须将数据分成几个较小的请求，并将这些较小的请求发送到一个或多个 i/o 目标。 用于处理这种情况的方法包括：

-   调用 [**IWDFDevice：： CreateRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest) 以创建一个其他请求对象，该对象表示一个较小的请求。

    驱动程序可以将此请求同步发送到 i/o 目标。 较小的请求的 [**IRequestCallbackRequestCompletion：： OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) 回调函数可以调用 [**IWDFIoRequest2：：重用**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse) ，以便驱动程序可以重用该请求并再次将其发送到 i/o 目标。 在 i/o 目标完成较小的请求后， **OnCompletion** 回调函数可以调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 删除驱动程序创建的请求对象，驱动程序可以调用 [**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 来完成原始请求。

-   调用 [**IWDFDevice：： CreateRequest**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest) 以创建多个表示较小请求的请求对象。

    驱动程序的 i/o 目标可以异步处理多个较小的请求。 驱动程序可以为每个较小的请求注册一个 [**OnCompletion**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) 回调函数。 每次调用 **OnCompletion** 回调函数时，它都可以调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 删除驱动程序创建的请求对象。 在 i/o 目标完成所有较小的请求之后，驱动程序可以调用 [**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete) 来完成原始请求。

### <a name="obtaining-completion-information"></a>获取完成信息

若要获取有关另一驱动程序已完成的 i/o 请求的信息，可以：

-   使用 [**IWDFRequestCompletionParams**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfrequestcompletionparams) 接口可获取 i/o 请求的完成状态和其他信息。

-   使用 [**IWDFIoRequestCompletionParams**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequestcompletionparams) 接口可获取 i/o 请求的内存缓冲区。

-   使用 [**IWDFUsbRequestCompletionParams**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbrequestcompletionparams) 接口可获取内存缓冲区，以及与发送到 USB 目标管道对象的请求相关的其他信息。

此外，基于 UMDF 的驱动程序可以使用 [**IWDFIoRequest2：： GetStatus**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getstatus) 方法来获取 i/o 请求的当前状态（在请求完成之前或之后）。

 

