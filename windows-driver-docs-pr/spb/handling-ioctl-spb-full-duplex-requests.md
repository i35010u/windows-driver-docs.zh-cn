---
title: 处理 IOCTL_SPB_FULL_DUPLEX 请求
description: 某些总线，如 SPI，可在总线控制器和总线上的设备之间同时进行读取和写入传输。
ms.assetid: B200461F-9F9C-43A7-BA78-0864FD58C64E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d22ffe83193f03c36d258383ef8fd00b17d7fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843369"
---
# <a name="handling-ioctl_spb_full_duplex-requests"></a>处理 IOCTL\_SPB\_完整\_双工请求


某些总线，如 SPI，可在总线控制器和总线上的设备之间同时进行读取和写入传输。 为了支持这些全双工传输，简单外围总线（SPB） i/o 请求接口的定义包括： [**IOCTL\_SPB\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)i/o 控制代码（IOCTL）。 仅在硬件中实现全双工传输的总线控制器的 SPB 控制器驱动程序应支持**IOCTL\_SPB\_完整\_双工**IOCTL。

如果 SPB 控制器驱动程序支持全双工传输的 i/o 请求，则驱动程序应使用**IOCTL\_SPB\_为这些请求提供完整\_双工**IOCTL，并遵循本主题。 这些指南的目的是在支持**IOCTL\_SPB\_完全\_双工**请求的所有硬件平台之间鼓励统一的行为。 然后，连接到 SPB 的外围设备的驱动程序可以依赖于这些请求来产生类似的结果，而不管它们在哪个平台上运行。

## <a name="buffer-requirements"></a>缓冲区要求


[**Ioctl\_spb\_FULL\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)请求的格式与[**ioctl\_SPB\_执行\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求的格式相同，但有以下限制：

-   请求中[ **\_传输\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)结构的 SPB 必须只包含两个条目。 第一个条目描述包含要写入设备的数据的缓冲区。 第二个条目描述用于保存从设备读取的数据的缓冲区。
-   传输列表中的每个[**SPB\_传输\_列表\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry)结构必须指定**DelayInUs**值为零。

在全双工传输过程中，读取和写入传输开始统一。 写入数据的第一个字节与读取数据的第一个字节同时在总线上传输。

IOCTL\_SPB 中的写入和读取缓冲区 **\_完整\_双工**请求的长度不必相同。

如果读取缓冲区的长度小于写入缓冲区，则全双工总线传输将继续，直到写入缓冲区的全部内容写入设备为止。 读取缓冲区已满后，总线控制器会丢弃从设备接收到的所有其他数据，直至全双工总线传输完成。

如果写入缓冲区短于读取缓冲区，则全双工总线传输将继续，直到读取缓冲区已满。 写入缓冲区的全部内容写入设备后，总线控制器会将零写入设备，直至全双工总线传输完成。

如果**IOCTL\_SPB\_完整\_双工**请求成功完成，则 SPB 控制器驱动程序会将 i/o 状态块的**状态**成员设置为 "成功"\_状态，并将**信息**成员设置为全双工传输过程中传输的总字节数（读取的字节数加上写入的字节数）。 **信息**成员中的计数值绝不应超过读取缓冲区大小和写入缓冲区大小之和。

如果读取缓冲区的长度小于写入缓冲区，则**信息**成员中的计数值不应包含总线控制器从设备读取的数据的字节数（以及在读取缓冲区已满后丢弃的数据）。 例如，如果使用1字节写入缓冲区和4字节读取缓冲区的全双工传输成功完成，则计数值应为5，而不是8。 同样，如果写入缓冲区短于读取缓冲区，则计数值不应包含在清空写入缓冲区后写入设备的零。

## <a name="parameter-checking"></a>参数检查


尽管[**IOCTL\_spb\_执行\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)和**IOCTL\_SPB\_完全\_双工**请求的格式类似，但使用 SPB 框架扩展（SpbCx）对其进行不同的处理。 对于**IOCTL\_SPB\_执行\_序列**请求，SpbCx 验证请求中的参数值，并在请求发起方的进程上下文中捕获请求的缓冲区。 SpbCx 通过驱动程序的[*EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence)回调函数（专用于这些请求）将 IOCTL\_spb 传递给 spb 控制器驱动程序 **\_执行\_序列**请求。

与此相反，SpbCx 将 IOCTL\_SPB 视为自定义的、驱动程序定义的 IOCTL 请求 **\_完整\_双工**请求。 SpbCx 通过驱动程序的[*EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)回调函数将 IOCTL\_spb 传递给 spb 控制器驱动程序 **\_完整\_双工**请求，后者还处理驱动程序支持的任何自定义 IOCTL 请求。 SpbCx 不对这些请求进行参数检查或缓冲区捕获。 驱动程序负责通过其*EvtSpbControllerIoOther*函数接收的 IOCTL 请求可能需要的任何参数检查或缓冲区捕获。 若要启用缓冲区捕获，驱动程序必须在驱动程序注册其*EvtSpbControllerIoOther*函数时提供[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。 有关详细信息，请参阅[为自定义 IOCTLs 使用**SPB\_传输\_列表**结构](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)。




通常，SPB 控制器驱动程序在*EvtSpbControllerIoOther*函数中验证 IOCTL\_SPB 中的参数值， **\_完整\_双工**请求，而不是在*EvtIoInCallerContext*函数中。 下面的代码示例演示了驱动程序如何实现参数检查。 在此示例中，驱动程序将验证是否满足以下参数要求：

-   请求中的传输列表仅包含两个条目。
-   传输列表中的第一个条目适用于写入缓冲区，第二个条目用于读取缓冲区。
-   这两个条目的**DelayInUs**值为零。

```cpp
//
// Validate the transfer count.
//

SPB_REQUEST_PARAMETERS params;
SPB_REQUEST_PARAMETERS_INIT(&params);
SpbRequestGetParameters(SpbRequest, &params);

if (params.SequenceTransferCount != 2)
{
    //
    // The full-duplex request must have 
    // exactly two transfer descriptors.
    //
    
    status = STATUS_INVALID_PARAMETER;        
    goto exit;
}

//
// Retrieve the write and read transfer descriptors.
//

const ULONG fullDuplexWriteIndex = 0;
const ULONG fullDuplexReadIndex = 1;

SPB_TRANSFER_DESCRIPTOR writeDescriptor;
SPB_TRANSFER_DESCRIPTOR readDescriptor;
PMDL pWriteMdl;
PMDL pReadMdl;

SPB_TRANSFER_DESCRIPTOR_INIT(&writeDescriptor);
SPB_TRANSFER_DESCRIPTOR_INIT(&readDescriptor);

SpbRequestGetTransferParameters(
    SpbRequest, 
    fullDuplexWriteIndex, 
    &writeDescriptor,
    &pWriteMdl);

SpbRequestGetTransferParameters(
    SpbRequest, 
    fullDuplexReadIndex, 
    &readDescriptor,
    &pReadMdl);
    
//
// Validate the transfer direction of each descriptor.
//

if ((writeDescriptor.Direction != SpbTransferDirectionToDevice) ||
    (readDescriptor.Direction != SpbTransferDirectionFromDevice))
{
    //
    // For full-duplex I/O, the direction of the first transfer
    // must be SpbTransferDirectionToDevice, and the direction
    // of the second must be SpbTransferDirectionFromDevice.
    //
    
    status = STATUS_INVALID_PARAMETER;
    goto exit;
}

//
// Validate the delay for each transfer descriptor.
//

if ((writeDescriptor.DelayInUs != 0) || (readDescriptor.DelayInUs != 0))
{
    //
    // The write and read buffers for full-duplex I/O are transferred
    // simultaneously over the bus. The delay parameter in each transfer
    // descriptor must be set to 0.
    //
    
    status = STATUS_INVALID_PARAMETER;
    goto exit;
}

MyDriverPerformFullDuplexTransfer(
    pDevice, 
    pRequest,
    writeDescriptor,
    pWriteMdl,
    readDescriptor,
    pReadMdl);
```

检查参数值之后，上面的代码示例调用名为 `MyDriverPerformFullDuplexTransfer`的驱动程序内部例程来启动全双工 i/o 传输。

 

 




