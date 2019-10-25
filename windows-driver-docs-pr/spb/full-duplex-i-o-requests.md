---
title: 全双工 I/O 请求
description: 某些总线，如 SPI，支持全双工总线传输。
ms.assetid: C80FE3F2-6659-4DE8-8F77-F77EDA60400F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c6c9054a0fc18acc01cbeaa842220f10d64d392
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826170"
---
# <a name="full-duplex-io-requests"></a>全双工 I/O 请求


某些总线，如 SPI，支持全双工总线传输。 这些传输通过将数据同时写入设备并从同一设备读取数据来提高 i/o 性能。 为了支持全双工总线传输，[简单外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（SPB） [i/o 请求接口](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))定义了[**IOCTL\_SPB\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)i/o 控制代码（IOCTL）。

支持**IOCTL\_SPB\_完整\_双工**IOCTL 是可选的。 仅在硬件中实现全双工传输的总线控制器的[SPB 控制器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)支持此 IOCTL。 如果 SPB 控制器驱动程序不支持全双工传输，则该驱动程序将无法通过所有**IOCTL\_SPB\_其接收的完整\_双工**请求，并将其完成，并将错误状态代码状态\_not\_受.

## <a name="transfer-list"></a>传输列表


**Ioctl\_spb\_完整\_双工**请求的格式类似于[**ioctl\_SPB\_执行\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求的格式。 这两个请求都使用[**SPB\_传输\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)结构来描述请求的读取和写入传输列表。 IOCTL\_SPB 中的传输列表 **\_执行\_序列**请求可以有任意组合的读取缓冲区和写入缓冲区。 与此相反， **IOCTL\_SPB\_完整\_双工**请求的传输列表必须始终只有一个读取缓冲区和一个写入缓冲区。 写入缓冲区始终是转换列表中的第一个缓冲区，读取缓冲区是第二个缓冲区。

对**IOCTL\_SPB 的额外要求\_完整\_双工**请求，是**DelayInUs**成员在 spb 中必须始终为零[ **\_传输\_列表\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry)结构读取缓冲区和写入缓冲区。

下面的代码示例演示了 SPB 外围设备的驱动程序如何为 IOCTL\_SPB 构建传输列表， **\_完整\_双工**请求。

```cpp
const ULONG transfers = 2;

SPB_TRANSFER_LIST_AND_ENTRIES(transfers) seq;
SPB_TRANSFER_LIST_INIT(&(seq.List), transfers);

{
    ULONG index = 0;
    seq.List.Transfers[index] = SPB_TRANSFER_LIST_ENTRY_INIT_SIMPLE(
        SpbTransferDirectionToDevice,
        0,
        pWriteBuffer,
        writeBufferLength);

    seq.List.Transfers[index + 1] = SPB_TRANSFER_LIST_ENTRY_INIT_SIMPLE(
        SpbTransferDirectionFromDevice,
        0,
        pReadBuffer,
        readBufferLength);
}
```

前面的代码示例使用了[**SPB\_传输\_列表\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_init) and [**spb\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_entry_init_simple)\_\_INIT\_简单函数初始化传输列表标头和日志. Spb\_传输在 Spb 头文件中定义的 **\_LIST\_和\_条目**宏，简化了传输列表的声明。 此宏将 `seq` 变量定义为一个结构，该结构包含一个 **\_传输\_列表**结构和一个**spb\_传输\_\_项**数组的两个元素。

## <a name="full-duplex-bus-transfers"></a>全双工总线传输


为了响应 IOCTL\_SPB\_从 SPB 外设驱动程序的**完整\_双工**请求，SPB 控制器驱动程序会在总线上启动全双工传输。 写入缓冲区的第一个字节会在总线时钟的相同时钟周期写入设备，在此期间，读取缓冲区的第一个字节将从设备中读取。

IOCTL\_SPB 的读取缓冲区和写入缓冲区 **\_完整\_双工**请求的长度不必相同。 如果写入缓冲区小于读取缓冲区，则在清空缓冲区后，SPB 控制器驱动程序停止将写入缓冲区的内容写入到设备，但会继续填充读取缓冲区，直到它已满。 同样，如果读取缓冲区小于写入缓冲区，则 SPB 控制器驱动程序会在读取缓冲区已满后停止填充它，但会继续将写入缓冲区的内容写入设备，直到缓冲区被清空。

## <a name="example-kmdf-driver"></a>示例： KMDF 驱动程序


用于 SPB 外围设备的内核模式 Driver Foundation （KMDF）驱动程序将调用一个方法（如[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) ），将 IOCTL 请求发送到 SPB 控制器。 此方法具有*InputBuffer*和*OutputBuffer*参数。 对于某些类型的设备，驱动程序可能会将这两个参数分别指向写入缓冲区和读取缓冲区，以用于 IOCTL 请求。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将*InputBuffer*参数设置为指向\_列表结构中指向 SPB 的内存描述符 **\_传输**。 例如，对于**IOCTL\_SPB\_完整\_双工**请求，此结构描述写入缓冲区和读取缓冲区（按该顺序）。 驱动程序将*OutputBuffer*参数设置为 NULL。

下面的代码示例演示了一个**WdfIoTargetSendIoctlSynchronously**调用，该调用将**IOCTL\_SPB 发送\_完整\_双工**请求到 SPB 外围设备。 在此示例中，`seq` 变量是在[传输列表](#transfer-list)的代码示例中定义的传输列表。

```cpp
ULONG_PTR BytesTransferred = 0;
NTSTATUS Status;
  
WDF_MEMORY_DESCRIPTOR MemoryDescriptor;
WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(
                            &MemoryDescriptor,  
                            &seq,  
                            sizeof(seq));

Status = WdfIoTargetSendIoctlSynchronously(
                            SpbIoTarget,
                            NULL,
                            IOCTL_SPB_FULL_DUPLEX,
                            &MemoryDescriptor,  // InputBuffer
                            NULL,               // OutputBuffer
                            NULL,
                            &BytesTransferred);
```

在上面的代码示例中，`MemoryDescriptor` 变量是一个框架内存说明符。 [**WDF\_内存\_描述符\_INIT\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)宏将初始化此描述符，以充当 `seq` 变量中包含的结构的容器。 在对**WdfIoTargetSendIoctlSynchronously**方法的调用中，`SpbIoTarget` 变量是先前在总线上打开的目标外围设备的句柄。 此方法的*InputBuffer*参数是指向内存说明符的指针。 *OutputBuffer*参数为 NULL。

此代码示例中的**WdfIoTargetSendIoctlSynchronously**调用将 `BytesTransferred` 变量设置为传输的总字节数（写入的字节数加上读取的字节数）。 例如，如果请求具有1字节的写入缓冲区和4字节的读取缓冲区，并且调用成功，则 `BytesTransferred` 值应为5。

## <a name="example-umdf-driver"></a>示例： UMDF 驱动程序


适用于 SPB 外围设备的用户模式 Driver Foundation （UMDF）驱动程序调用方法（如[**IWDFIoTarget：： FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) ）来格式化 i/o 控制操作的 i/o 请求。 此方法具有*pInputMemory*和*pOutputMemory*参数。 某些类型的设备的驱动程序可能使用这两个参数来指向读取缓冲区和 IOCTL 请求的写入缓冲区。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将*pInputMemory*参数设置为指向包含**SPB\_传输\_列表**结构的内存对象。 例如，此结构描述用于**IOCTL\_SPB\_完整\_双工**请求的写入缓冲区和读取缓冲区。 驱动程序将*pOutputMemory*参数设置为 NULL。

下面的代码示例演示了**IWDFIoTarget：： FormatRequestForIoctl**调用，该调用将**IOCTL\_SPB\_完整\_双工**请求的格式设置为 spb 外围设备。 在此示例中，`seq` 变量是在[传输列表](#transfer-list)的代码示例中定义的传输列表。

```cpp
ULONG_PTR BytesTransferred = 0;
HRESULT hr;

pWdfMemory->SetBuffer(seq, sizeof(seq));

hr = pWdfRemoteTarget->FormatRequestForIoctl( 
                         pWdfIoRequest,
                         IOCTL_SPB_FULL_DUPLEX,
                         NULL,
                         pWdfMemory,  // pInputMemory
                         NULL,        // pOutputMemory 
                         NULL,
                         NULL);

if (FAILED(hr))
{
    goto exit;
}

hr = pWdfIoRequest->Send(pRemoteTarget,
                         WDF_REQUEST_SEND_OPTION_SYNCHRONOUS,
                         0);

if (FAILED(hr))
{
    goto exit;
}

{
    IWDFRequestCompletionParams* pWdfParams = 0;

    pWdfIoRequest->GetCompletionParams(&pWdfParams);
    hr = pWdfParams->GetCompletionStatus();
    if (SUCCEEDED(hr))
    {
        BytesTransferred = pWdfParams->GetInformation();
    }
    SAFE_RELEASE(pWdfParams);
}
```

前面的代码示例使用以下对象指针：

-   `pWdfMemory` 变量是指向以前分配的框架内存（[**IWDFMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)）对象的指针。 外围设备驱动程序使用此对象作为 `seq` 变量中的传输列表的容器。
-   `pWdfRemoteTarget` 参数是指向以前打开的远程 i/o 目标（[**IWDFRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)）对象的指针。 此对象表示外围设备驱动程序与外围设备的连接。
-   `pWdfIoRequest` 变量是指向之前创建的框架请求（[**IWDFIoRequest2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest2)）对象的指针。 外围设备驱动程序使用此对象作为**IOCTL\_SPB 的容器\_完整\_双工**请求。

前面的代码示例执行以下操作：

1.  对[**IWDFMemory：： SetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)方法的调用会重复使用所 `pWdfMemory` 指向的内存对象，以用作传输列表的容器。
2.  **FormatRequestForIoctl**调用重复使用所 `pWdfIoRequest` 指向的请求对象，以用作**IOCTL\_SPB 的容器\_完全\_双工**请求。 此方法的*pInputMemory*参数是一个指针，指向包含传输列表的内存对象。 *POutputMemory*参数为 NULL。
3.  调用[**IWDFIoRequest：： Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)方法会将 i/o 请求发送到设备。 此调用是同步的，并在 SPB 控制器驱动程序完成请求后返回。
4.  对[**IWDFIoRequest：： GetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)方法的调用从请求获取完成参数。
5.  对[**IWDFRequestCompletionParams：： GetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfrequestcompletionparams-getinformation)方法的调用从完成参数（i/o 状态块中的**信息**字段）获取*信息*值。 此值是**IOCTL\_SPB\_完整\_双工**请求传输的总字节数（写入的字节数加上读取的字节数）。

 

 




