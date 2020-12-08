---
title: 使用常用缓冲区
description: 使用常用缓冲区
keywords:
- DMA 操作 WDK KMDF，常见缓冲区
- 总线主控 DMA WDK KMDF，常见缓冲区
- 常见缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 102b9ee97f672f2f4e6f3b2babaee2a952e7ebdc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821099"
---
# <a name="using-common-buffers"></a>使用常用缓冲区


\[仅适用于 KMDF\]




DMA 设备的驱动程序有时必须分配设备和驱动程序都可以访问的缓冲空间。 例如，设备可能将传输信息（如字节计数）写入此缓冲区空间，驱动程序可以读取该信息以确定传输的字节数。 这种类型的缓冲区空间称为 *公共缓冲区*。

若要分配公用缓冲区，驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数：

-   调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) 创建 DMA 启用程序对象。

-   调用 [**WdfCommonBufferCreate**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreate) 或 [**WdfCommonBufferCreateWithConfig**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig) 以创建缓冲区。

-   调用 [**WdfCommonBufferGetAlignedLogicalAddress**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedlogicaladdress) 获取缓冲区的逻辑地址，设备可以访问该地址。

-   调用 [**WdfCommonBufferGetAlignedVirtualAddress**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedvirtualaddress) 以获取缓冲区的虚拟地址，驱动程序可以访问该地址。

下面的代码示例是从 [PLX9x5x](/samples/browse/)示例的 *Init .c* 文件中获取的。 此代码显示了 KMDF 驱动程序如何分配通用缓冲空间。

```cpp
// Allocate common buffer for building writes
DevExt->WriteCommonBufferSize = 
         sizeof( DMA_TRANSFER_ELEMENT) * DevExt->WriteTransferElements;
status = WdfCommonBufferCreate( DevExt->DmaEnabler,
                                DevExt->WriteCommonBufferSize,
                                WDF_NO_OBJECT_ATTRIBUTES, 
                                &DevExt->WriteCommonBuffer );
if (!NT_SUCCESS(status)) {
    . . . //Error-handling code omitted 
    }
DevExt->WriteCommonBufferBase = 
             WdfCommonBufferGetAlignedVirtualAddress(
                      DevExt->WriteCommonBuffer);
DevExt->WriteCommonBufferBaseLA = 
             WdfCommonBufferGetAlignedLogicalAddress(
                      DevExt->WriteCommonBuffer);
RtlZeroMemory( DevExt->WriteCommonBufferBase, DevExt->WriteCommonBufferSize);
```

如果在调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)之前驱动程序调用 [**WdfDeviceSetAlignmentRequirement**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement) ，则 **WdfDmaEnablerCreate** 创建的缓冲区将与驱动程序指定给 **WdfDeviceSetAlignmentRequirement** 的内存地址边界对齐。 否则，公共缓冲区会与 word 地址边界对齐。 或者，驱动程序可以调用 [**WdfCommonBufferCreateWithConfig**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig) 来指定单个缓冲区的对齐方式。

若要获取驱动程序已分配的公用缓冲区的长度，驱动程序可以调用 [**WdfCommonBufferGetLength**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetlength)。

当驱动程序使用公用缓冲区完成时，驱动程序将调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。
