---
title: 处理 IOCTL_SPB_FULL_DUPLEX 请求
description: 某些总线，如 SPI，可在总线控制器和总线上的设备之间同时进行读取和写入传输。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f25fde99c2e9648b31b8e22cf9feb9249caf132e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804841"
---
# <a name="handling-ioctl_spb_full_duplex-requests"></a>处理 IOCTL \_ SPB \_ 全双工 \_ 请求


某些总线，如 SPI，可在总线控制器和总线上的设备之间同时进行读取和写入传输。 为了支持这些全双工传输，简单外围总线 (SPB) i/o 请求接口的定义包括了一个选项，即 [**ioctl \_ SPB \_ 全双工 \_**](https://msdn.microsoft.com/library/windows/hardware/hh974774) i/o 控制代码 (ioctl) 。 仅在硬件中实现全双工传输的总线控制器的 SPB 控制器驱动程序应支持 **IOCTL \_ SPB \_ 全双工 \_** IOCTL。

如果 SPB 控制器驱动程序支持全双工传输的 i/o 请求，则驱动程序应为这些请求使用 **IOCTL \_ SPB \_ 全双工 \_** ioctl，并应遵循本主题中介绍的实现准则。 这些指南的目的是在支持 **IOCTL \_ SPB \_ 全双工 \_** 请求的所有硬件平台之间鼓励统一的行为。 然后，连接到 SPB 的外围设备的驱动程序可以依赖于这些请求来产生类似的结果，而不管它们在哪个平台上运行。

## <a name="buffer-requirements"></a>缓冲区要求


[**Ioctl \_ spb \_ 全双工 \_**](https://msdn.microsoft.com/library/windows/hardware/hh974774)请求的格式与 [**ioctl \_ spb \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求的格式相同，但具有以下限制：

-   请求中的 [**SPB \_ 传输 \_ 列表**](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list) 结构必须只包含两个条目。 第一个条目描述包含要写入设备的数据的缓冲区。 第二个条目描述用于保存从设备读取的数据的缓冲区。
-   传输列表中的每个 [**SPB \_ 传输 \_ 列表 \_ 条目**](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry) 结构都必须指定 **DelayInUs** 值为零。

在全双工传输过程中，读取和写入传输开始统一。 写入数据的第一个字节与读取数据的第一个字节同时在总线上传输。

**IOCTL \_ SPB \_ 全双工 \_** 请求中的写入和读取缓冲区的长度不必相同。

如果读取缓冲区的长度小于写入缓冲区，则全双工总线传输将继续，直到写入缓冲区的全部内容写入设备为止。 读取缓冲区已满后，总线控制器会丢弃从设备接收到的所有其他数据，直至全双工总线传输完成。

如果写入缓冲区短于读取缓冲区，则全双工总线传输将继续，直到读取缓冲区已满。 写入缓冲区的全部内容写入设备后，总线控制器会将零写入设备，直至全双工总线传输完成。

如果 **IOCTL \_ SPB \_ 全双工 \_** 请求成功完成，则 SPB 控制器驱动程序会将 i/o 状态块的 **状态** 成员设置为 "成功" 状态 \_ ，并将 **信息** 成员设置为在全双工传输过程中传输 (字节数的字节总数加上写入) 。 **信息** 成员中的计数值绝不应超过读取缓冲区大小和写入缓冲区大小之和。

如果读取缓冲区的长度小于写入缓冲区，则 **信息** 成员中的计数值不应包含总线控制器从设备读取的数据的字节 (，并在读取缓冲区满后放弃) 。 例如，如果使用1字节写入缓冲区和4字节读取缓冲区的全双工传输成功完成，则计数值应为5，而不是8。 同样，如果写入缓冲区短于读取缓冲区，则计数值不应包含在清空写入缓冲区后写入设备的零。

## <a name="parameter-checking"></a>参数检查


虽然 [**ioctl \_ spb \_ 执行 \_ 顺序**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 和 **ioctl \_ spb \_ 全双工 \_** 请求具有相似的格式，但它们的处理方式不同于 SPB 框架扩展 (SpbCx) 。 对于 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求，SpbCx 将验证请求中的参数值，并在请求发起方的进程上下文中捕获请求的缓冲区。 SpbCx 通过驱动程序的 [*EvtSpbControllerIoSequence*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence)回调函数向 SPB 控制器驱动程序传递 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求，该函数专用于这些请求。

与此相反，SpbCx 将 **IOCTL \_ SPB \_ 全双工 \_** 请求视为自定义的、驱动程序定义的 IOCTL 请求。 SpbCx 通过驱动程序的 [*EvtSpbControllerIoOther*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)回调函数将 **IOCTL \_ SPB \_ \_** 全双工请求传递给 spb 控制器驱动程序，后者还处理驱动程序支持的任何自定义 IOCTL 请求。 SpbCx 不对这些请求进行参数检查或缓冲区捕获。 驱动程序负责通过其 *EvtSpbControllerIoOther* 函数接收的 IOCTL 请求可能需要的任何参数检查或缓冲区捕获。 若要启用缓冲区捕获，驱动程序必须在驱动程序注册其 *EvtSpbControllerIoOther* 函数时提供 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。 有关详细信息，请参阅 [为自定义 IOCTLs 使用 **SPB \_ 传输 \_ 列表** 结构](./using-the-spb-transfer-list-structure.md)。




通常，SPB 控制器驱动程序在 *EvtSpbControllerIoOther* 函数而不是 *EvtIoInCallerContext* 函数中验证 **IOCTL \_ SPB \_ 全双工 \_** 请求中的参数值。 下面的代码示例演示了驱动程序如何实现参数检查。 在此示例中，驱动程序将验证是否满足以下参数要求：

-   请求中的传输列表仅包含两个条目。
-   传输列表中的第一个条目适用于写入缓冲区，第二个条目用于读取缓冲区。
-   这两个条目的 **DelayInUs** 值为零。

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

检查参数值之后，上面的代码示例调用名为的驱动程序内部例程 `MyDriverPerformFullDuplexTransfer` 来启动全双工 i/o 传输。

 

