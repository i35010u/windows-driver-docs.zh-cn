---
title: 同步发送 I/O 请求
description: 同步发送 I/O 请求
ms.assetid: e7e9f2d2-afc5-439b-8a04-72d117114fae
keywords:
- 常规 I/O 面向 WDK KMDF，I/O 将请求发送到
- 发送 I/O 请求 WDK KMDF
- 发送的 I/O 请求 WDK KMDF，同步
- 以同步方式发送 I/O 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2df1beb7b971cea9ca326e29c1d9afb2f632df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325145"
---
# <a name="sending-io-requests-synchronously"></a>同步发送 I/O 请求





下表列出了您的驱动程序可以调用以同步方式将 I/O 请求发送到的 I/O 目标的 I/O 目标对象方法。 有关如何使用这些方法的详细信息，请参阅这些方法的参考页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">方法</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548669" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548669)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p></td>
<td align="left"><p>将发送的读取的请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548672" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548672)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left"><p>发送一个写请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548660" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548660)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p></td>
<td align="left"><p>发送设备控制请求</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548656" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548656)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p></td>
<td align="left"><p>发送内部设备控制请求</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548651" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548651)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left"><p>发送的非标准的内部设备控制请求</p></td>
</tr>
</tbody>
</table>

 

您还可以发送请求以同步方式通过调用[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)，但您必须先按照中所述的规则将格式化请求[发送 I/O 请求以异步方式](sending-i-o-requests-asynchronously.md)。

以同步方式将 I/O 请求发送到的 I/O 目标是比将 I/O 请求发送到程序更简单[异步](sending-i-o-requests-asynchronously.md)。 但是，应使用以下准则来帮助您决定同步 I/O 是否适合于您的驱动程序：

-   如果您的驱动程序不会发送多个 I/O 请求，则可以使用同步 I/O，如果不减少了系统或设备的性能，因为您的驱动程序在等待每个 I/O 请求完成。

-   如果您的驱动程序必须处理多个 I/O 请求以短的时间段，可能不能允许您的驱动程序要等待的每个请求发送的下一个请求之前完成。 否则为您的驱动程序可能会丢失数据，或者降低其设备 （和可能是，整个系统） 的性能。 在这种情况下，异步 I/O 可能更好的选择。

-   同步 I/O 可用于处理操作，必须启动并完成而无需其他并发活动。 此类操作可能包括重置 USB 管道或读取设备注册。

-   大多数时候，调用对象方法以同步方式发送的 I/O 请求时，您的驱动程序应指定一个超时值。 如果您的驱动程序未指定超时值，以及如果是设备或较低级别驱动程序无法响应，可以停止正在您的驱动程序。 因此，用户可以体验的无响应的应用程序。 此外，其他驱动程序可能无法获取系统资源，例如[的工作项](using-framework-work-items.md)，如果您的驱动程序没有释放它们。

-   如果驱动程序的上方和下方你堆栈中需要操作继续进行同步，您的驱动程序应使用同步 I/O。 因此，应了解可能存在于驱动程序堆栈中其他驱动程序的要求。

下面的示例演示如何将发送一个同步 I/O 控制 (IOCTL) 请求：

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

 

 





