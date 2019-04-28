---
title: 全双工 I/O 请求
description: 某些总线，例如 SPI，支持完全双工总线传输。
ms.assetid: C80FE3F2-6659-4DE8-8F77-F77EDA60400F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c9aad36345ec0e46e4ab2677cf66c112a6ae485
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348061"
---
# <a name="full-duplex-io-requests"></a>全双工 I/O 请求


某些总线，例如 SPI，支持完全双工总线传输。 这些传输提高 I/O 性能数据写入到设备，同时在同一设备读取数据。 若要支持全双工总线传输[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)（存储） [I/O 请求接口](https://msdn.microsoft.com/library/windows/hardware/hh698224)定义[ **IOCTL\_存储\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774) I/O 控制代码 (IOCTL)。

为支持**IOCTL\_存储\_完整\_双工**IOCTL 是可选的。 仅[存储控制器驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh698220)的总线在硬件中实现全双工传输的控制器都支持此 IOCTL。 如果存储控制器驱动程序不支持完全双工传输，此驱动程序失败，所有**IOCTL\_存储\_完整\_双工**请求它接收并完成它们时的错误状态代码状态\_不\_受支持。

## <a name="transfer-list"></a>传输列表


格式**IOCTL\_存储\_完整\_双工**请求是类似于[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求。 这两个请求使用[**存储\_传输\_列表**](https://msdn.microsoft.com/library/windows/hardware/hh406221)结构描述列表读取和写入请求的传输。 中的传输列表**IOCTL\_存储\_EXECUTE\_序列**请求可以具有的读取缓冲区和写入缓冲区的任意组合。 与此相反，传输列表中**IOCTL\_存储\_完整\_双工**请求必须始终具有恰好一个读取的缓冲区和一个写入缓冲区。 写入缓冲区始终是第一个缓冲区中的传输列表中，并且读取的缓冲区是第二个。

还要求**IOCTL\_存储\_完整\_双工**请求是**DelayInUs**成员必须始终为零的[ **存储\_传输\_列表\_条目**](https://msdn.microsoft.com/library/windows/hardware/hh406223)描述读取的缓冲区和写入缓冲区的结构。

下面的代码示例显示了如何存储外围设备的驱动程序生成的传输列表**IOCTL\_存储\_完整\_双工**请求。

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

前面的代码示例使用[**存储\_传输\_列表\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/hh406224)并[**存储\_传输\_列表\_条目\_INIT\_简单**](https://msdn.microsoft.com/library/windows/hardware/hh406214)函数来初始化传输列出标头和条目。 **存储\_传输\_列表\_AND\_条目**宏，Spb.h 标头文件中定义，简化了传输列表的声明。 此宏可定义`seq`变量为结构，其中包含**存储\_传输\_列表**结构和一个**存储\_传输\_列表\_条目**两个元素的数组。

## <a name="full-duplex-bus-transfers"></a>全双工总线传输


以响应**IOCTL\_存储\_完整\_双工**从存储外围设备驱动程序存储控制器驱动程序将启动全双工传输总线上的请求。 写入缓冲区的第一个字节写入到设备上的总线时钟在其读取缓冲区的第一个字节从设备读取的相同刻度线。

读取的缓冲区和写入缓冲区**IOCTL\_存储\_完整\_双工**请求不需要是相同的长度。 如果写入缓冲区小于读取缓冲区，存储控制器驱动程序将停止写入缓冲区的内容写入到设备后缓冲区为空，但会继续以填充读取的缓冲区，直到它已满。 同样，如果读取的缓冲区小于写入缓冲区，将停止存储控制器驱动程序后它已满，但仍然无法写入设备的写入缓冲区的内容，直到清空缓冲区填充读取的缓冲区。

## <a name="example-kmdf-driver"></a>例如：KMDF 驱动程序


存储外围设备的内核模式驱动程序的基础 (KMDF) 驱动程序调用的方法，如[ **WdfIoTargetSendIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548660)将 IOCTL 请求发送到存储控制器。 此方法具有*InputBuffer*并*OutputBuffer*参数。 对于某些类型的设备驱动程序可能会使用这两个参数以指向写入缓冲区和读取的缓冲区中，分别为 IOCTL 请求。 但是，若要将 IOCTL 请求发送到的存储控制器，存储外围设备驱动程序集*InputBuffer*参数以指向指向的内存描述符**存储\_传输\_列表**结构。 例如，此结构描述同时写入缓冲区和读取的缓冲区 （按此顺序） **IOCTL\_存储\_完整\_双工**请求。 驱动程序集*OutputBuffer*参数为 NULL。

下面的代码示例演示**WdfIoTargetSendIoctlSynchronously**调用将发送**IOCTL\_存储\_完整\_双工**存储外围设备的请求设备。 `seq`在此示例中的变量是传输列表中的代码示例中定义[传输列表](#transfer-list)。

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

在前面的代码示例中，`MemoryDescriptor`变量是框架内存描述符。 [ **WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552393)宏初始化此说明符作为结构的容器中包含`seq`变量。 在调用**WdfIoTargetSendIoctlSynchronously**方法，`SpbIoTarget`变量是目标外围设备总线上的以前打开句柄。 *InputBuffer*给此方法的参数是指向内存描述符。 *OutputBuffer*参数为 NULL。

**WdfIoTargetSendIoctlSynchronously**在此调用的代码示例设置`BytesTransferred`总字节数的变量传输 （写入的字节数加上读取字节）。 例如，如果请求具有 1 个字节写入缓冲区和 4 字节的读取的缓冲区，并在调用成功，`BytesTransferred`值应为 5。

## <a name="example-umdf-driver"></a>例如：UMDF 驱动程序


存储外围设备的用户模式驱动程序的基础 (UMDF) 驱动程序调用的方法，如[ **IWDFIoTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)格式化 I/O 控制操作的 I/O 请求。 此方法具有*pInputMemory*并*pOutputMemory*参数。 对于某些类型的设备驱动程序可能会使用这两个参数以指向读取的缓冲区和 IOCTL 请求写入缓冲区。 但是，若要将 IOCTL 请求发送到的存储控制器，存储外围设备驱动程序集*pInputMemory*参数，以对内存对象，其中包含指向**存储\_传输\_列表**结构。 例如，此结构描述写入缓冲区和读取的缓冲区**IOCTL\_存储\_完整\_双工**请求。 驱动程序集*pOutputMemory*参数为 NULL。

下面的代码示例演示**IWDFIoTarget::FormatRequestForIoctl**格式的调用**IOCTL\_存储\_完整\_双工**到存储的请求外围设备。 `seq`在此示例中的变量是传输列表中的代码示例中定义[传输列表](#transfer-list)。

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

前面的代码示例使用以下对象的指针：

-   `pWdfMemory`变量是指向以前分配的框架内存的指针 ([**IWDFMemory**](https://msdn.microsoft.com/library/windows/hardware/ff559249)) 对象。 外围设备驱动程序使用此对象作为容器中的传输列表`seq`变量。
-   `pWdfRemoteTarget`参数是指向以前打开的远程 I/O 目标 ([**IWDFRemoteTarget**](https://msdn.microsoft.com/library/windows/hardware/ff560247)) 对象。 此对象表示与外围设备的外围设备驱动程序的连接。
-   `pWdfIoRequest`变量是指向以前创建的框架请求 ([**IWDFIoRequest2**](https://msdn.microsoft.com/library/windows/hardware/ff558988)) 对象。 外围设备驱动程序使用此对象作为容器**IOCTL\_存储\_完整\_双工**请求。

前面的代码示例将执行以下操作：

1.  在调用[ **IWDFMemory::SetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff560162)方法重复使用通过指向的内存对象`pWdfMemory`作为传输列表的容器。
2.  **FormatRequestForIoctl**调用重用指向请求对象`pWdfIoRequest`若要充当容器**IOCTL\_存储\_完整\_双工**请求。 *PInputMemory*给此方法的参数是指向包含传输列表的内存对象。 *POutputMemory*参数为 NULL。
3.  在调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法将 I/O 请求发送到设备。 此调用是同步的并且存储控制器驱动程序完成请求后返回。
4.  在调用[ **IWDFIoRequest::GetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff559084)方法从请求获取完成参数。
5.  在调用[ **IWDFRequestCompletionParams::GetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff560305)方法获取*信息*从完成的参数的值 ( **信息**I/O 状态块中的字段)。 此值是传输的字节数 （写入的字节数加上读取的字节数） 的总数**IOCTL\_存储\_完整\_双工**请求。

 

 




