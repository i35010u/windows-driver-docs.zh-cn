---
title: 使用常用缓冲区
description: 使用常用缓冲区
ms.assetid: 81a56f62-917e-4798-b2cc-6469c802fab8
keywords:
- DMA 操作 WDK KMDF，常见的缓冲区
- 主总线 DMA WDK KMDF，常见的缓冲区
- 常见缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cc731c6c5b715894f07cc51796d005d055e771
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372284"
---
# <a name="using-common-buffers"></a>使用常用缓冲区


\[仅适用于 KMDF\]




有时 DMA 设备的驱动程序必须分配的设备和驱动程序可以访问的缓冲区空间。 例如，设备可能会写入传输信息，例如在字节计数，到此缓冲区空间和驱动程序可以读取它以确定已传输的字节数。 此类型的缓冲区空间称为*常见缓冲区*。

若要分配将常见缓冲区，您的驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数：

-   调用[ **WdfDmaEnablerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)创建 DMA 推动器对象。

-   调用[ **WdfCommonBufferCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreate)或[ **WdfCommonBufferCreateWithConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)创建缓冲区。

-   调用[ **WdfCommonBufferGetAlignedLogicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedlogicaladdress)获取缓冲区的逻辑地址，设备可以访问。

-   调用[ **WdfCommonBufferGetAlignedVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetalignedvirtualaddress)获取缓冲区的虚拟地址，驱动程序可访问。

下面的代码示例摘自*Init.c*的文件[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例。 此代码演示如何 KMDF 驱动程序分配常见缓冲区空间。

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

如果您的驱动程序调用[ **WdfDeviceSetAlignmentRequirement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetalignmentrequirement)之前调用[ **WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)，缓冲区该**WdfDmaEnablerCreate**创建到指定的驱动程序的内存地址边界对齐**WdfDeviceSetAlignmentRequirement**。 否则，常见的缓冲区地址词的边界对齐。 或者，驱动程序可以调用[ **WdfCommonBufferCreateWithConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)指定一个缓冲区的对齐方式。

若要获取您的驱动程序已分配的常见缓冲区的长度，该驱动程序可以调用[ **WdfCommonBufferGetLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffergetlength)。

该驱动程序完成后使用常见的缓冲区，驱动程序调用[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)。









