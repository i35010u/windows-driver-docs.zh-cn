---
title: 内存缓冲区生命周期
description: 内存缓冲区生命周期
ms.assetid: abf43bf5-a4a3-4aeb-9ec5-3458252933d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43f1c4245044babf93efccbe70810ec21c110f9f
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734315"
---
# <a name="memory-buffer-life-cycle"></a>内存缓冲区生命周期


内存缓冲区的生命周期跨越从创建缓冲区到删除缓冲区的时间。 本主题介绍缓冲区使用方案以及它们在删除缓冲区时的影响。

在内核模式驱动程序框架 (KMDF) 中，请求对象表示 i/o 请求。 每个请求对象与一个或多个内存对象相关联，每个内存对象都表示一个用于请求中的输入或输出的缓冲区。

当框架创建用于表示传入 i/o 请求的请求和内存对象时，它会将请求对象设置为关联内存对象的父级。 因此，内存对象的持续时间不能长于请求对象的生存期。 当基于框架的驱动程序完成 i/o 请求时，框架会删除请求对象和内存对象，因此，这两个对象的句柄变为无效。

但是，基础缓冲区是不同的。 根据创建缓冲区的组件及其创建缓冲区的方式，缓冲区可能具有引用计数，并且可能由内存对象拥有，也可能不是。 如果内存对象拥有缓冲区，则该缓冲区将具有引用计数，并且它的生存期限制为内存对象的生存期。 如果某个其他组件创建了缓冲区，则该缓冲区的生存期和内存对象不相关。

基于框架的驱动程序还可以创建自己的请求对象以发送到 i/o 目标。 驱动程序创建的请求可以重复使用驱动程序在 i/o 请求中收到的现有内存对象。 经常向 i/o 目标发送请求的驱动程序可以 [重复使用它创建的请求对象](reusing-framework-request-objects.md) 。

若要确保驱动程序不会尝试引用无效的句柄或缓冲区指针，请了解请求对象、内存对象和基础缓冲区的生存期。

请考虑以下使用方案：

-   方案1： [驱动程序接收来自 KMDF 的 i/o 请求，处理该请求并完成该请求](#scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it)。
-   方案2： [驱动程序接收来自 KMDF 的 i/o 请求并将其转发给 i/o 目标](#scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target)。
-   方案3： [驱动程序发出使用现有内存对象的 i/o 请求](#scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object)。
-   方案4： [驱动程序发出的 i/o 请求使用新的内存对象。](#scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object)
-   方案5： [驱动程序重用它创建的请求对象。](#scenario-5-driver-reuses-a-request-object-that-it-created)

## <a name="scenario-1-driver-receives-an-io-request-from-kmdf-handles-it-and-completes-it"></a>方案1：驱动程序接收来自 KMDF 的 i/o 请求，处理该请求并完成该请求。

在最简单的方案中，KMDF 将请求发送到驱动程序，该驱动程序将执行 i/o 并完成请求。 在这种情况下，可能已由用户模式应用程序、其他驱动程序或操作系统本身创建了基础缓冲区。 有关如何访问缓冲区的信息，请参阅 [在基于框架的驱动程序中访问数据缓冲区](./accessing-data-buffers-in-wdf-drivers.md)。

当驱动程序 [完成请求](completing-i-o-requests.md)时，框架会删除内存对象。 然后，该缓冲区指针无效。

## <a name="scenario-2-driver-receives-an-io-request-from-kmdf-and-forwards-it-to-an-io-target"></a>方案2：驱动程序接收来自 KMDF 的 i/o 请求并将其转发给 i/o 目标。

在此方案中，驱动程序将 [请求转发](forwarding-i-o-requests.md) 到 i/o 目标。 下面的示例代码演示了驱动程序如何从传入的请求对象中检索内存对象的句柄，格式化发送到 i/o 目标的请求，并发送请求：

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

当 i/o 目标完成请求时，框架将调用为请求设置的驱动程序的完成回调。 下面的代码演示了一个简单的完成回调：

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

当驱动程序从其完成回调调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 时，框架会删除内存对象。 驱动程序检索的内存对象句柄现在无效。

## <a name="scenario-3-driver-issues-an-io-request-that-uses-an-existing-memory-object"></a>方案3：驱动程序发出使用现有内存对象的 i/o 请求。


某些驱动程序发出自己的 i/o 请求，并将它们发送到 i/o 目标，这些目标由 i/o 目标对象表示。 驱动程序可以创建自己的请求对象，也可以 [重复使用框架创建的请求对象](reusing-framework-request-objects.md)。 使用任一种方法，驱动程序都可以重复使用以前请求中的内存对象。 驱动程序不得更改基础缓冲区，但它可以在对新 i/o 请求进行格式化时传递缓冲区偏移量。

有关如何设置使用现有内存对象的新 i/o 请求的格式的信息，请参阅 [向常规 I/o 目标发送 I/o 请求](sending-i-o-requests-to-general-i-o-targets.md)。

当框架设置发送到 i/o 目标的请求的格式时，它将代表 i/o 目标对象对回收的内存对象进行引用。 在执行下列操作之一之前，i/o 目标对象会保留此引用：

-   请求已完成。
-   该驱动程序通过调用 *WdfIoTargetFormatRequestXxx* 或 *WdfIoTargetSendXxxSynchronously* 方法之一重新格式化请求对象。 有关这些方法的详细信息，请参阅 [框架 I/o 目标对象方法](/windows-hardware/drivers/ddi/wdfiotarget/)。
-   驱动程序调用 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)。

新的 i/o 请求完成后，框架将调用此请求的驱动程序设置的 i/o 完成回调。 此时，i/o 目标对象仍保留对该内存对象的引用。 因此，在 i/o 完成回调中，驱动程序必须先在驱动程序创建的请求对象上调用 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse) ，然后才能完成从中检索内存对象的原始请求。 如果驱动程序未调用 **WdfRequestReuse**，则会由于额外的引用而发生 bug 检查。

## <a name="scenario-4-driver-issues-an-io-request-that-uses-a-new-memory-object"></a>方案4：驱动程序发出的 i/o 请求使用新的内存对象。


框架为驱动程序提供了三种方法来创建新的内存对象，具体取决于基础缓冲区的源。 有关详细信息，请参阅 [使用内存缓冲区](using-memory-buffers.md)。

如果缓冲区是由框架或从驱动程序创建的 [后备链表列表](using-memory-buffers.md#using-lookaside-lists)分配的，则内存对象拥有缓冲区，因此只要内存对象存在，缓冲区指针就会保持有效。 发出异步 i/o 请求的驱动程序应始终使用内存对象所拥有的缓冲区，这样框架就可以确保在 i/o 请求已完成到发出驱动程序之前，缓冲区一直存在。

如果驱动程序通过调用 [**WdfMemoryCreatePreallocated**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)将以前分配的缓冲区分配给新的内存对象，则该内存对象不拥有该缓冲区。 在这种情况下，内存对象的生存期和基础缓冲区的生存期不相关。 驱动程序必须管理缓冲区的生存期，并且不能尝试使用无效的缓冲区指针。

## <a name="scenario-5-driver-reuses-a-request-object-that-it-created"></a>方案5：驱动程序重用它创建的请求对象。


驱动程序可以重复使用它创建的请求对象，但必须在每次重复使用之前通过调用 [**WdfRequestReuse**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse) 来重新初始化每个此类对象。 有关详细信息，请参阅 [重复使用框架请求对象](reusing-framework-request-objects.md)。

有关重新初始化请求对象的代码示例，请参阅随 KMDF 版本一起提供的 [Toaster](/samples/browse/) 和 [NdisEdge](/samples/browse/) 示例。