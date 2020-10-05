---
title: 编写 64 位音频驱动程序
description: 编写 64 位音频驱动程序
ms.assetid: 0b4cbb98-506e-443f-bac2-59dbdbcb1798
keywords:
- 音频驱动程序 WDK，64位
- 64位 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498670d4444f69b9cd461c10b13c418cf7b44fef
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733539"
---
# <a name="writing-64-bit-audio-drivers"></a>编写 64 位音频驱动程序


## <span id="writing_64_bit_audio_drivers"></span><span id="WRITING_64_BIT_AUDIO_DRIVERS"></span>


如果你正在编写64位驱动程序或编写可编译为在32和64位系统上运行的驱动程序，请遵循 [驱动程序编程方法](../kernel/using-ntstatus-values.md)中的迁移指南。 下面介绍了编写64位音频驱动程序时可能会遇到的一些缺陷。

首先，在现有32位驱动程序代码中查找的潜在问题是指针类型和整数类型（如 DWORD 或 ULONG）之间的转换。 具有为32位计算机编写代码的程序员可能用于假设指针值适合 DWORD 值或 ULONG。 对于64位代码，此假设是危险的。 将指针转换为类型 DWORD 或 ULONG 可能导致截断64位指针。 更好的方法是将指针转换为类型 DWORD \_ ptr 或 ULONG \_ ptr。 类型为 DWORD \_ ptr 或 ULONG ptr 的无符号整数 \_ 始终足够大以存储整个指针，无论代码是针对32还是64位计算机编译的。

例如， [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp) 指针字段 **IoStatus**。**信息** 的类型为 ULONG \_ PTR。 下面的代码演示将64位指针值复制到此字段时不会执行的操作：

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG)pDeviceRelations;  // wrong
```

此代码示例错误地将 `pDeviceRelations` 指针转换为类型 ULONG，这可以在时截断指针值 `sizeof(pDeviceRelations) > sizeof(ULONG)` 。 正确的方法是将指针转换为 ULONG \_ PTR，如下所示：

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG_PTR)pDeviceRelations;  // correct
```

这会保留指针值的所有64位。

资源列表以物理地址类型的结构存储资源的物理地址 \_ (参阅 [IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)) 。 若要避免截断64位地址，应在将地址复制到结构或从结构中读取地址时访问结构的 **QuadPart** 成员而不是其 **LowPart** 成员。 例如， **FindTranslatedPort** 宏返回指向 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor) 结构的指针，该结构包含 i/o 端口的基址。 **U**。**端口**。此结构的**开始**成员是 \_ 指向基址的物理地址指针。 下面的代码演示了不执行的操作：

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.LowPart;  // wrong
```

同样，这可能会截断指针。 相反，你应该访问此成员的 **QuadPart** ，如下所示：

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.QuadPart;  // correct
```

这会复制整个64位指针。

内联 Win64 函数（如 **PtrToUlong** 和 **UlongToPtr** ）在指针和整数类型之间安全转换，而不依赖于这些类型的相对大小假设。 如果一种类型的长度较短，则必须在转换为较长的类型时进行扩展。 是否通过使用符号位填充来扩展较短的类型或是否为每个 Win64 函数定义了零。 这意味着任何代码段（例如

```cpp
    ULONG ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // wrong
```

应该替换为

```cpp
    ULONG_PTR ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // correct
```

这是首选方案，尽管 `ulSlotPhysAddr` 可能表示只是32而不是64位的硬件寄存器的值。 有关在指针和整数类型之间进行转换的所有新的 Win64 helper 函数的列表，请参阅 [新的数据类型](../kernel/the-new-data-types.md)。

