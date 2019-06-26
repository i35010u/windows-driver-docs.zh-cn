---
title: 编写 64 位音频驱动程序
description: 编写 64 位音频驱动程序
ms.assetid: 0b4cbb98-506e-443f-bac2-59dbdbcb1798
keywords:
- 音频驱动程序 WDK，64 位
- 64 位 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a028cbf0dc3d08cd18d82c5e76b41f7f1bb295
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364773"
---
# <a name="writing-64-bit-audio-drivers"></a>编写 64 位音频驱动程序


## <span id="writing_64_bit_audio_drivers"></span><span id="WRITING_64_BIT_AUDIO_DRIVERS"></span>


如果要编写的 64 位驱动程序或编写可编译为两个 32 位和 64 位系统上运行的驱动程序，按照中的移植指南[驱动程序的编程技术](https://docs.microsoft.com/windows-hardware/drivers/kernel/miscellaneous-driver-programming-techniques)。 下面介绍了一些在编写的 64 位的音频驱动程序可能会遇到的缺陷。

首先，这在现有的 32 位驱动程序代码中查找的潜在问题是指针类型和如 DWORD 或 ULONG 的整数类型之间的转换。 与编写代码的 32 位计算机的经验的程序员可能习惯于假定适合 DWORD 或 ULONG 的指针值。 对于 64 位代码，这一假设是危险的。 强制转换为类型 DWORD 或 ULONG 的指针可能会导致将 64 位指针被截断。 更好的方法是强制转换指针类型 DWORD\_PTR 或 ULONG\_PTR。 无符号的整数的类型为 DWORD\_PTR 或 ULONG\_PTR 始终有足够空间来存储整个指针，而不考虑是否会将代码编译为 32 位或 64 位计算机。

例如， [ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)指针字段**IoStatus**。**信息**是类型为 ULONG\_PTR。 下面的代码演示要不执行的操作时将一个 64 位指针值复制到此字段：

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG)pDeviceRelations;  // wrong
```

此代码示例会错误地将强制转换`pDeviceRelations`指向类型 ULONG，如果可以截断该指针值的指针`sizeof(pDeviceRelations) > sizeof(ULONG)`。 正确的方法是将强制转换为 ULONG 的指针\_PTR，如以下所示：

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG_PTR)pDeviceRelations;  // correct
```

这样可保留所有 64 位指针值。

资源列表将资源的物理地址存储在一个结构类型物理\_地址 (请参阅[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iresourcelist))。 若要避免截断 64 位地址，您应访问的结构**QuadPart**成员而非其**LowPart**成员时将一个地址复制到结构或读取中的地址结构。 例如， **FindTranslatedPort**宏将返回一个指向[ **CM\_部分\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_partial_resource_descriptor)结构，它包含 I/O 端口的基址。 **U**。**端口**。**启动**此结构的成员是物理\_到基址的地址指针。 下面的代码演示要不执行的操作：

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.LowPart;  // wrong
```

同样，这可以截断该指针。 相反，应访问**QuadPart**此成员，如以下所示：

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.QuadPart;  // correct
```

这会复制整个 64 位指针。

之类的函数内联 Win64 **PtrToUlong**并**UlongToPtr**安全地指针和整数类型之间转换而不依赖于这些类型的相对大小假设。 如果短于另一种类型，必须将转换为时间类型时扩展。 是否在较短类型可通过扩展是明确定义为每个 Win64 函数符号位或用零填充。 这意味着，任何代码段如

```cpp
    ULONG ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // wrong
```

应替换为

```cpp
    ULONG_PTR ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // correct
```

这是首选即使`ulSlotPhysAddr`可能表示为仅 32 硬件寄存器的值而不是 64 位长。 所有新 Win64 帮助程序函数的指针和整数类型之间进行转换的列表，请参阅[新的数据类型](https://docs.microsoft.com/windows-hardware/drivers/kernel/the-new-data-types)。

 

 




