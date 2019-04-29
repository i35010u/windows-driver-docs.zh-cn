---
title: 内存缓冲区生命周期
description: 内存缓冲区生命周期
ms.assetid: abf43bf5-a4a3-4aeb-9ec5-3458252933d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa982e9b3612562a0e22700df672e9ffaf6be436
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390166"
---
# <a name="memory-buffer-life-cycle"></a>内存缓冲区生命周期


内存缓冲区的生命周期的范围为从缓冲区创建时到被删除时的时间。 本主题介绍缓冲区的使用方案以及它们如何影响时删除缓冲区。

在内核模式驱动程序框架 (KMDF)，请求对象表示的 I/O 请求。 每个请求对象所关联具有一个或多个内存对象和内存的每个对象都表示一个缓冲区，用于输入或输出请求中。

当 framework 创建请求和内存来表示传入的 I/O 请求的对象时，它会设置为相关联的内存对象的父级的请求对象。 因此，可以不会请求对象的生存期超过保留的内存对象。 基于框架的驱动程序完成 I/O 请求，框架就会删除请求对象，该内存对象，因此对这两个对象的句柄无效。

但是，基础缓冲区是不同的。 具体取决于哪个组件创建缓冲区以及它如何创建缓冲区，缓冲区可能具有引用计数，并可能拥有的内存对象，或它可能不会。 如果内存对象拥有缓冲区，然后缓冲区的引用计数并将限制为内存对象的生存期。 如果某些其他组件创建缓冲区，然后将缓冲区和内存对象的生存期不相关。

基于框架的驱动程序还可以创建其自己的请求对象发送到 I/O 目标。 驱动程序创建请求可以重复使用该驱动程序接收的 I/O 请求中的现有内存对象。 频繁地将请求发送到 I/O 目标的驱动程序可以[重复使用的请求对象](reusing-framework-request-objects.md)它创建的。

了解请求对象，该内存对象和基础缓冲区的生存期很重要，以确保您的驱动程序不会尝试引用无效的句柄或缓冲区指针。

请考虑以下使用方案：

-   方案 1：[驱动程序接收来自 KMDF 的 I/O 请求、 处理它，并完成后，它](#scenario-1-driver-receives-an-i-o-request-from-kmdf-handles-it-and-completes-it)。
-   方案 2：[驱动程序收到来自 KMDF 的 I/O 请求并将其转发到 I/O 目标](#scenario-2-driver-receives-an-i-o-request-from-kmdf-and-forwards-it-to-an-i-o-target)。
-   方案 3：[驱动程序将发出使用一个现有的内存对象的 I/O 请求](#scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object)。
-   方案 4:[驱动程序将发出 I/O 请求使用新的内存对象。](#scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object)
-   方案 5:[驱动程序将重新使用它创建一个请求对象。](#scenario-5-driver-reuses-a-request-object-that-it-created)

## <a name="scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it"></a>方案 1：驱动程序接收来自 KMDF 的 I/O 请求、 处理它，并完成后，它。

在最简单的方案中，KMDF 调度对驱动程序，它执行 I/O，并完成请求的请求。 在这种情况下，基础缓冲区可能已创建的用户模式应用程序，另一个驱动程序或操作系统本身。 有关如何对访问缓冲区的信息，请参阅[基于 Framework 的驱动程序中访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff540701)。

当驱动程序[完成请求](completing-i-o-requests.md)，框架将删除内存对象。 缓冲区指针然后是无效的。

## <a name="scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target"></a>方案 2：驱动程序收到来自 KMDF 的 I/O 请求，并将其转发到 I/O 的目标。

在此方案中，该驱动程序[会将请求转发](forwarding-i-o-requests.md)到 I/O 的目标。 下面的示例代码显示了一个驱动程序从传入的请求对象检索到内存对象的句柄、 设置格式的请求将发送到 I/O 目标，并发送请求：

```cpp
VOID
EvtIoRead(
    IN WDFQUEUE Queue,
    IN WDFREQUEST Request,
    IN size_t Length
    )
{
    NTSTATUS status;
    WDFMEMORY memory;
    WDFIOTARGET ioTarget;
    BOOLEAN ret;
    ioTarget = WdfDeviceGetIoTarget(WdfIoQueueGetDevice(Queue));

    status = WdfRequestRetrieveOutputMemory(Request, &memory);
    if (!NT_SUCCESS(status)) {
        goto End;
    }

    status = WdfIoTargetFormatRequestForRead(ioTarget,
                                    Request,
                                    memory,
                                    NULL,
                                    NULL);
    if (!NT_SUCCESS(status)) {
        goto End;
    }

    WdfRequestSetCompletionRoutine(Request,
                                    RequestCompletionRoutine,
                                    WDF_NO_CONTEXT);

    ret = WdfRequestSend (Request, ioTarget, WDF_NO_SEND_OPTIONS);
    if (!ret) {
        status = WdfRequestGetStatus (Request);
        goto End;
    }

    return;

End:
    WdfRequestComplete(Request, status);
    return;

}
```

I/O 目标已完成请求，框架将调用驱动程序将设置为请求的完成回调。 下面的代码演示一个简单的完成回调：

```cpp
VOID
RequestCompletionRoutine(
    IN WDFREQUEST                  Request,
    IN WDFIOTARGET                 Target,
    PWDF_REQUEST_COMPLETION_PARAMS CompletionParams,
    IN WDFCONTEXT                  Context
    )
{
    UNREFERENCED_PARAMETER(Target);
    UNREFERENCED_PARAMETER(Context);

    WdfRequestComplete(Request, CompletionParams->IoStatus.Status);

    return;

}
```

当驱动程序调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)从其完成回调，该框架将删除内存对象。 该驱动程序检索到的内存对象句柄现在是无效的。

## <a name="scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object"></a>方案 3：驱动程序将发出使用一个现有的内存对象的 I/O 请求。


某些驱动程序发出其自己的 I/O 请求，并将其发送到由 I/O 目标对象表示的 I/O 目标。 该驱动程序可以创建其自己的请求对象或[重用框架创建请求对象](reusing-framework-request-objects.md)。 使用两种方法之一，则可以重复驱动程序使用的前一个请求的内存对象。 该驱动程序不能更改基础缓冲区，但它可以将传递的缓冲区偏移量时设置新的 I/O 请求的格式。

有关如何设置使用现有的内存对象的新 I/O 请求的格式信息，请参阅[将 I/O 请求发送到常规 I/O 目标](sending-i-o-requests-to-general-i-o-targets.md)。

当框架格式的请求将发送到 I/O 目标时，这除去了代表 I/O 目标对象回收的内存对象的引用。 I/O 目标对象将保留此引用，直到发生以下操作之一：

-   请求已完成。
-   该驱动程序会重新设置格式的请求对象再次通过调用之一*WdfIoTargetFormatRequestXxx*或*WdfIoTargetSendXxxSynchronously*方法。 有关这些方法的详细信息，请参阅[Framework I/O 目标对象方法](https://msdn.microsoft.com/library/windows/hardware/dn265644)。
-   驱动程序调用[ **WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)。

新的 I/O 请求完成后，框架将调用该驱动程序设置此请求的 I/O 完成回调。 此时，I/O 目标对象仍保留的引用，对内存对象。 因此，在 I/O 完成回调中，该驱动程序必须调用[ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026)驱动程序创建请求对象，它完成从其检索到内存的原始请求之前对象。 如果该驱动程序不会调用**WdfRequestReuse**，错误是由于的额外引用导致的 bug 检查。

## <a name="scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object"></a>方案 4:驱动程序将发出 I/O 请求使用新的内存对象。


该框架提供三种方法来创建新的内存对象，具体取决于基础缓冲区的源的驱动程序。 有关详细信息，请参阅[使用的内存缓冲区](using-memory-buffers.md)。

由框架或从驱动程序创建，如果分配缓冲区[后备](using-memory-buffers.md#using-lookaside-lists)，内存对象拥有缓冲区，因此，只要该内存对象存在缓冲区指针保持有效。 发出异步 I/O 请求的驱动程序应始终使用所拥有的内存对象，以便该框架可以确保缓冲区持续，直到返回到颁发的驱动程序已完成的 I/O 请求的缓冲区。

如果该驱动程序将以前分配的缓冲区分配给新的内存对象，通过调用[ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)，内存对象不拥有缓冲区。 在这种情况下，内存对象的生存期和基础缓冲区的生存期无关。 驱动程序必须管理的缓冲区的生存期，一定不要尝试使用无效的缓冲区指针。

## <a name="scenario-5-driver-reuses-a-request-object-that-it-created"></a>方案 5:驱动程序将重新使用它创建一个请求对象。


驱动程序可以重复使用它创建的请求对象，但它必须通过调用重新初始化每个此类对象[ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026)之前每个重复使用。 有关详细信息，请参阅[重用 Framework 请求对象](reusing-framework-request-objects.md)。

有关重新初始化请求对象的示例代码，请参阅[Toaster](https://go.microsoft.com/fwlink/p/?linkid=256195)并[NdisEdge](https://go.microsoft.com/fwlink/p/?linkid=256154) KMDF 与提供的示例版本。









