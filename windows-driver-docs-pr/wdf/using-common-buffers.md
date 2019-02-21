---
title: 使用常见的缓冲区
description: 使用常见的缓冲区
ms.assetid: 81a56f62-917e-4798-b2cc-6469c802fab8
keywords:
- DMA 操作 WDK KMDF，常见的缓冲区
- 主总线 DMA WDK KMDF，常见的缓冲区
- 常见缓冲区 WDK KMDF
- 缓冲区 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc15afc844dd6e06befcb323d28df6437f922ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526991"
---
# <a name="using-common-buffers"></a>使用常见的缓冲区


\[仅适用于 KMDF\]




有时 DMA 设备的驱动程序必须分配的设备和驱动程序可以访问的缓冲区空间。 例如，设备可能会写入传输信息，例如在字节计数，到此缓冲区空间和驱动程序可以读取它以确定已传输的字节数。 此类型的缓冲区空间称为*常见缓冲区*。

若要分配将常见缓冲区，您的驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数：

-   调用[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983)创建 DMA 推动器对象。

-   调用[ **WdfCommonBufferCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545800)或[ **WdfCommonBufferCreateWithConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff545805)创建缓冲区。

-   调用[ **WdfCommonBufferGetAlignedLogicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff545814)获取缓冲区的逻辑地址，设备可以访问。

-   调用[ **WdfCommonBufferGetAlignedVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff545820)获取缓冲区的虚拟地址，驱动程序可访问。

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

如果您的驱动程序调用[ **WdfDeviceSetAlignmentRequirement** ](https://msdn.microsoft.com/library/windows/hardware/ff546861)之前调用[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)，缓冲区该**WdfDmaEnablerCreate**创建到指定的驱动程序的内存地址边界对齐**WdfDeviceSetAlignmentRequirement**。 否则，常见的缓冲区地址词的边界对齐。 或者，驱动程序可以调用[ **WdfCommonBufferCreateWithConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff545805)指定一个缓冲区的对齐方式。

若要获取您的驱动程序已分配的常见缓冲区的长度，该驱动程序可以调用[ **WdfCommonBufferGetLength**](https://msdn.microsoft.com/library/windows/hardware/ff545828)。

该驱动程序完成后使用常见的缓冲区，驱动程序调用[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)。









