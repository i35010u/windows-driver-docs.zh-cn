---
title: 处理 IOCTL_SPB_FULL_DUPLEX 请求
description: 某些总线，SPI，例如启用读取和写入传输总线控制器和总线上的设备之间同时发生。
ms.assetid: B200461F-9F9C-43A7-BA78-0864FD58C64E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3c535226f6e57ad27718b01537ea4fd438ca0c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385230"
---
# <a name="handling-ioctlspbfullduplex-requests"></a>处理 IOCTL\_存储\_完整\_双工请求


某些总线，SPI，例如启用读取和写入传输总线控制器和总线上的设备之间同时发生。 若要支持这些全双工传输，简单的外围总线 （存储） I/O 请求接口的定义包括，作为一个选项， [ **IOCTL\_存储\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774) I/O 控制代码 (IOCTL)。 仅存储控制器驱动程序的硬件中实现全双工传输总线控制器应支持**IOCTL\_存储\_完整\_双工**IOCTL。

如果存储控制器驱动程序支持完全双工传输 I/O 请求，应使用该驱动程序**IOCTL\_存储\_完整\_双工**IOCTL 这些请求，并应按照本主题中介绍的实现指导原则。 这些指南的目的是鼓励跨所有支持的硬件平台行为统一**IOCTL\_存储\_完整\_双工**请求。 然后，连接存储的外围设备的驱动程序可以依赖于这些请求以生成类似的结果，而不考虑它们运行在哪些平台。

## <a name="buffer-requirements"></a>缓冲区要求


[ **IOCTL\_存储\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)请求的格式相同[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求，但具有这些限制：

-   [**存储\_传输\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)请求中的结构必须包含正好两个条目。 第一项描述了包含要写入到设备的数据的缓冲区。 第二个条目描述用来保存从设备读取的数据缓冲区。
-   每个[**存储\_传输\_列表\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list_entry)传输列表中的结构必须指定**DelayInUs**值为零。

全双工传送期间，读取和写入传输启动更多信息。 写入数据的第一个字节通过总线传输读取数据的第一个字节时。

中的写入和读取缓冲区**IOCTL\_存储\_完整\_双工**请求不需要是相同的长度。

如果读取的缓冲区小于写入缓冲区，全双工总线传输将一直写入缓冲区的全部内容写入到设备。 读取的缓冲区已满后，总线控制器将放弃全双工总线传输完成之前，从设备收到的所有其他数据。

如果写入缓冲区是短于读取缓冲区，全双工总线传输将继续到读取的缓冲区变满为止。 写入缓冲区的全部内容写入到设备后，总线控制器将写入到设备的零，直到全双工总线传输完成。

如果**IOCTL\_存储\_完整\_双工**请求成功完成后，存储控制器驱动程序集**状态**I/O 状态块的状态的成员\_成功，并设置**信息**成员添加到总字节数在全双工传输过程中传输 （读取字节加上写入的字节数）。 中的计数值**信息**成员应永远不会超过读取的缓冲区大小和写入缓冲区大小的总和。

如果读取的缓冲区小于写入缓冲区，计数中的值**信息**成员应包括后读取的数据总线控制器从设备读取 （并放弃） 的字节缓冲区已满。 例如，如果使用 1 个字节写入缓冲区和 4 字节的全双工传输读取缓冲区成功完成，计数值应为 5，不是 8。 同样，如果写入缓冲区小于读取缓冲区，计数值不应包含写入到设备后清空写入缓冲区的零。

## <a name="parameter-checking"></a>参数检查


尽管[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)并**IOCTL\_存储\_完整\_双工**请求具有类似格式，存储框架扩展 (SpbCx) 的处理方式不同。 有关**IOCTL\_存储\_EXECUTE\_序列**请求，SpbCx 验证参数值在请求中，并捕获请求发起方的进程上下文中请求的缓冲区。 将传递 SpbCx **IOCTL\_存储\_EXECUTE\_序列**通过驱动程序的存储控制器驱动程序对请求[ *EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_sequence)回调函数，专用于这些请求。

与此相反，将视为 SpbCx **IOCTL\_存储\_完整\_双工**作为自定义、 驱动程序定义 IOCTL 请求的请求。 将传递 SpbCx **IOCTL\_存储\_完整\_双工**通过驱动程序的存储控制器驱动程序对请求[ *EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_other)回调函数，还可以处理的驱动程序支持的任何自定义 IOCTL 请求。 SpbCx 执行这些请求没有参数检查或缓冲区捕获。 该驱动程序负责检查任何参数或缓冲区捕获 IOCTL 可能需要的请求，该驱动程序将收到通过其*EvtSpbControllerIoOther*函数。 若要启用缓冲区捕获，驱动程序必须提供[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数时，驱动程序注册其*EvtSpbControllerIoOther*函数。 有关详细信息，请参阅[Using**存储\_传输\_列表**结构的自定义 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)。




通常情况下，存储控制器驱动程序将验证中的参数值**IOCTL\_存储\_完整\_双工**请求中*EvtSpbControllerIoOther*函数而不是在*EvtIoInCallerContext*函数。 下面的代码示例显示了该驱动程序可能会实现参数检查。 在此示例中，该驱动程序验证满足以下参数要求：

-   在请求中的传输列表包含两个条目。
-   传输列表中的第一个条目为写入缓冲区，第二个用于读取缓冲区。
-   **DelayInUs**这两个条目的值为零。

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

参数值后，上述代码示例的驱动程序内部调用例程，名为`MyDriverPerformFullDuplexTransfer`、 启动全双工 I/O 传输。

 

 




