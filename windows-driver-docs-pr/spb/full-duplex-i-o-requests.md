---
title: 全双工 I/O 请求
description: 某些总线，如 SPI，支持全双工总线传输。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9caeb6882d0a0492db4e2a7e4cbdc849698aa5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804855"
---
# <a name="full-duplex-io-requests"></a>全双工 I/O 请求


某些总线，如 SPI，支持全双工总线传输。 这些传输通过将数据同时写入设备并从同一设备读取数据来提高 i/o 性能。 为了支持全双工总线传输， [简单的外围总线](/previous-versions/hh450903(v=vs.85)) (SPB) [i/o 请求接口](/previous-versions/hh698224(v=vs.85)) 定义 ioctl [**\_ SPB \_ 全双工 \_**](https://msdn.microsoft.com/library/windows/hardware/hh974774) i/o 控制代码 (ioctl) 。

支持 **IOCTL \_ SPB \_ 全双工 \_** IOCTL 是可选的。 仅在硬件中实现全双工传输的总线控制器的 [SPB 控制器驱动程序](./spb-controller-drivers.md) 支持此 IOCTL。 如果 SPB 控制器驱动程序不支持全双工传输，则此驱动程序将无法接收到所有的 **IOCTL \_ SPB \_ \_** 全双工请求，并将其完成，并将错误状态代码状态 " \_ 不 \_ 受支持"。

## <a name="transfer-list"></a>传输列表


**Ioctl \_ spb \_ 全双工 \_** 请求的格式类似于 [**ioctl \_ spb \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求的格式。 这两个请求都使用 [**SPB \_ 传输 \_ 列表**](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list) 结构来描述请求的读取和写入传输列表。 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求中的传输列表可以具有读取缓冲区和写入缓冲区的任意组合。 与此相反， **IOCTL \_ SPB \_ 全双工 \_** 请求中的传输列表必须始终只有一个读取缓冲区和一个写入缓冲区。 写入缓冲区始终是转换列表中的第一个缓冲区，读取缓冲区是第二个缓冲区。

**IOCTL \_ SPB \_ 全双工 \_** 请求的另一个要求是， **DelayInUs** 成员必须在描述读取缓冲区和写入缓冲区的 [**SPB \_ 传输 \_ 列表 \_ 输入**](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry)结构中始终为零。

下面的代码示例演示了 SPB 外围设备的驱动程序如何为 **IOCTL \_ SPB \_ 全双工 \_** 请求生成传输列表。

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

前面的代码示例使用 [**SPB \_ 传输 \_ 列表 \_ init**](/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_init) 和 [**spb \_ 传输 \_ 列表 \_ 条目 \_ init \_ 简单**](/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_entry_init_simple) 函数初始化传输列表标头和条目。 在 Spb 头文件中定义的 **spb \_ 传输 \_ 列表 \_ 和 \_ 条目** 宏简化了传输列表的声明。 此宏将 `seq` 变量定义为包含 **SPB \_ 传输 \_ 列表** 结构的结构和两个元素的 **spb \_ 传输 \_ 列表 \_ 项** 数组。

## <a name="full-duplex-bus-transfers"></a>Full-Duplex 总线传输


为了响应来自 SPB 外围设备驱动程序的 **IOCTL \_ SPB \_ 全双工 \_** 请求，SPB 控制器驱动程序会在总线上启动全双工传输。 写入缓冲区的第一个字节会在总线时钟的相同时钟周期写入设备，在此期间，读取缓冲区的第一个字节将从设备中读取。

**IOCTL \_ SPB \_ 全双工 \_** 请求的读取缓冲区和写入缓冲区的长度不必相同。 如果写入缓冲区小于读取缓冲区，则在清空缓冲区后，SPB 控制器驱动程序停止将写入缓冲区的内容写入到设备，但会继续填充读取缓冲区，直到它已满。 同样，如果读取缓冲区小于写入缓冲区，则 SPB 控制器驱动程序会在读取缓冲区已满后停止填充它，但会继续将写入缓冲区的内容写入设备，直到缓冲区被清空。

## <a name="example-kmdf-driver"></a>示例： KMDF 驱动程序


用于 SPB 外围设备的 Kernel-Mode Driver Foundation (KMDF) 驱动程序将调用一个方法，例如 [**WdfIoTargetSendIoctlSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) ，将 IOCTL 请求发送到 spb 控制器。 此方法具有 *InputBuffer* 和 *OutputBuffer* 参数。 对于某些类型的设备，驱动程序可能会将这两个参数分别指向写入缓冲区和读取缓冲区，以用于 IOCTL 请求。 但是，若要将 IOCTL 请求发送到 SPB 控制器，则 SPB 外围设备驱动程序将 *InputBuffer* 参数设置为指向用于指向 **spb \_ 传输 \_ 列表** 结构的内存描述符。 例如，以下结构对 **IOCTL \_ SPB \_ 全双工 \_** 请求) 顺序描述了写入缓冲区和读取缓冲区 (。 驱动程序将 *OutputBuffer* 参数设置为 NULL。

下面的代码示例演示了向 SPB 外围设备发送 **IOCTL \_ SPB \_ 全双工 \_** 请求的 **WdfIoTargetSendIoctlSynchronously** 调用。 `seq`在此示例中，变量是在[传输列表](#transfer-list)的代码示例中定义的传输列表。

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

在上面的代码示例中， `MemoryDescriptor` 变量是一个框架内存说明符。 [**WDF \_ 内存 \_ 描述符 \_ 初始化 \_ 缓冲区**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)宏将初始化此描述符，以用作变量中包含的结构的容器 `seq` 。 在对 **WdfIoTargetSendIoctlSynchronously** 方法的调用中， `SpbIoTarget` 变量是之前打开的指向总线上的目标外围设备的句柄。 此方法的 *InputBuffer* 参数是指向内存说明符的指针。 *OutputBuffer* 参数为 NULL。

此代码示例中的 **WdfIoTargetSendIoctlSynchronously** 调用将 `BytesTransferred` 变量设置为 (传输的字节总数加上) 读取的字节数。 例如，如果请求具有1字节写入缓冲区和4字节读取缓冲区，并且调用成功，则 `BytesTransferred` 值应为5。

## <a name="example-umdf-driver"></a>示例： UMDF 驱动程序


适用于 SPB 外围设备的 User-Mode Driver Foundation (UMDF) 驱动程序调用方法，例如 [**IWDFIoTarget：： FormatRequestForIoctl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) ，以格式化 i/o 控制操作的 i/o 请求。 此方法具有 *pInputMemory* 和 *pOutputMemory* 参数。 某些类型的设备的驱动程序可能使用这两个参数来指向读取缓冲区和 IOCTL 请求的写入缓冲区。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将 *pInputMemory* 参数设置为指向包含 **SPB \_ 传输 \_ 列表** 结构的内存对象。 例如，此结构描述了用于 **IOCTL \_ SPB \_ 全双工 \_** 请求的写入缓冲区和读取缓冲区。 驱动程序将 *pOutputMemory* 参数设置为 NULL。

下面的代码示例演示了将 **IOCTL \_ SPB \_ 全双工 \_** 请求格式化为 SPB 外围设备的 **IWDFIoTarget：： FormatRequestForIoctl** 调用。 `seq`在此示例中，变量是在[传输列表](#transfer-list)的代码示例中定义的传输列表。

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

-   `pWdfMemory`变量是指向以前分配的框架内存 ([**IWDFMemory**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)) 对象的指针。 外围设备驱动程序使用此对象作为变量中的传输列表的容器 `seq` 。
-   `pWdfRemoteTarget`参数是指向之前打开的远程 i/o 目标 ([**IWDFRemoteTarget**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)) 对象的指针。 此对象表示外围设备驱动程序与外围设备的连接。
-   `pWdfIoRequest`变量是指向之前创建的框架请求 ([**IWDFIoRequest2**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest2)) 对象的指针。 外围设备驱动程序使用此对象作为 **IOCTL \_ SPB \_ 全双工 \_** 请求的容器。

前面的代码示例执行以下操作：

1.  对 [**IWDFMemory：： SetBuffer**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfmemory-setbuffer) 方法的调用会重复使用指向的内存对象， `pWdfMemory` 作为传输列表的容器。
2.  **FormatRequestForIoctl** 调用重用指向的请求对象 `pWdfIoRequest` ，作为 **IOCTL \_ SPB \_ 全双工 \_** 请求的容器。 此方法的 *pInputMemory* 参数是一个指针，指向包含传输列表的内存对象。 *POutputMemory* 参数为 NULL。
3.  调用 [**IWDFIoRequest：： Send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法会将 i/o 请求发送到设备。 此调用是同步的，并在 SPB 控制器驱动程序完成请求后返回。
4.  对 [**IWDFIoRequest：： GetCompletionParams**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams) 方法的调用从请求获取完成参数。
5.  对 [**IWDFRequestCompletionParams：： GetInformation**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfrequestcompletionparams-getinformation)方法的调用从 i/o 状态块) 的 **信息** 字段 (的完成参数获取 *信息* 值。 此值是由 **IOCTL \_ SPB \_ 全双工 \_** 请求) 写入 (字节数传输的总字节数。

 

