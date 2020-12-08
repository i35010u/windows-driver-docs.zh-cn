---
title: 同步发送 I/O 请求
description: 同步发送 I/O 请求
keywords:
- 一般 i/o 目标 WDK KMDF，将 i/o 请求发送到
- 发送 i/o 请求 WDK KMDF
- 发送 i/o 请求 WDK KMDF，同步
- 同步发送 i/o 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76b43c45efff367a09fe7d4f95e288da3ed987d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821177"
---
# <a name="sending-io-requests-synchronously"></a>同步发送 I/O 请求





下表列出了驱动程序可以调用以将 i/o 请求同步发送到 i/o 目标的 i/o 目标对象方法。 有关如何使用这些方法的详细信息，请参阅方法的参考页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">方法</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p></td>
<td align="left"><p>发送读取请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left"><p>发送写入请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p></td>
<td align="left"><p>发送设备控制请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p></td>
<td align="left"><p>发送内部设备控制请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left"><p>发送非标准内部设备控制请求</p></td>
</tr>
</tbody>
</table>

 

你还可以通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)来同步发送请求，但必须先按照 [发送 i/o 请求](sending-i-o-requests-asynchronously.md)中所述的规则来格式化请求。

与异步发送 i/o 请求相比，将 i/o 请求同步发送到 i/o 目标的 [方式](sending-i-o-requests-asynchronously.md)更简单。 但是，你应使用下列准则来帮助你确定同步 i/o 是否适用于你的驱动程序：

-   如果你的驱动程序未发送多个 i/o 请求，并且由于你的驱动程序等待每个 i/o 请求完成，则可以使用同步 i/o。

-   如果你的驱动程序必须在较短的时间内处理多个 i/o 请求，你可能无法允许驱动程序等待每个请求完成，然后再发送下一个请求。 否则，驱动程序可能会丢失数据或降低其设备的性能 (并且可能) 整个系统。 在这种情况下，异步 i/o 可能是更好的选择。

-   同步 i/o 用于处理必须启动和完成的操作，而无需其他并发活动。 此类操作可能包括重置 USB 管道或读取设备寄存器。

-   大多数情况下，当驱动程序调用发送 i/o 请求的对象方法时，您的驱动程序应指定超时值。 如果您的驱动程序未指定超时值，并且如果某个设备或较低级别的驱动程序未能响应，则您的驱动程序可以停止。 因此，用户可能会遇到无响应的应用程序。 此外，如果你的驱动程序未发布，则其他驱动程序可能无法获取系统资源，如 [工作项](using-framework-work-items.md)。

-   如果堆栈中的以上和下面的驱动程序需要操作以同步方式执行，则驱动程序应使用同步 i/o。 因此，您应该了解驱动程序堆栈中可能存在的其他驱动程序的要求。

下面的示例演示如何 (IOCTL) 请求发送同步 i/o 控件：

```cpp
NTSTATUS                status;
    WDF_MEMORY_DESCRIPTOR   inputDesc, outputDesc;
    PWDF_MEMORY_DESCRIPTOR  pInputDesc = NULL, pOutputDesc = NULL;
    ULONG_PTR               bytesReturned;

    UNREFERENCED_PARAMETER(FileObject);

    if (InputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&inputDesc,
                                    InputBuffer,
                                    InputBufferLength);
        pInputDesc = &inputDesc;
    }

    if (OutputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&outputDesc,
                                    OutputBuffer,
                                    OutputBufferLength);
        pOutputDesc = &outputDesc;
    }

    status = WdfIoTargetSendIoctlSynchronously(
                        IoTarget,
                        WDF_NO_HANDLE, // Request
                        IoctlControlCode,
                        pInputDesc,
                        pOutputDesc,
                        NULL, // PWDF_REQUEST_SEND_OPTIONS
                        &bytesReturned);
    if (!NT_SUCCESS(status)) {
         DEBUGP(MP_ERROR,
        ("WdfIoTargetSendIoctlSynchronously failed 0x%x\n",
          status));
    }

    *BytesReadOrWritten = (ULONG)bytesReturned;
```

