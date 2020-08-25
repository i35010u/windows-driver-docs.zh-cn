---
title: 写 64 位打印机驱动程序
description: 写 64 位打印机驱动程序
ms.assetid: 41f1a521-980e-4ccd-a395-e1d1bf0114d1
keywords:
- 打印机驱动程序 WDK，64位
- 64位 WDK 打印机
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: cf731292ae5a10a34a5511dda4921bc75348dd58
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850292"
---
# <a name="writing-64-bit-printer-drivers"></a>写 64 位打印机驱动程序

如果你编写的是64位驱动程序或编写可编译为在32位和64位系统上运行的驱动程序，请遵循将 [驱动程序移植到64位 Windows](https://docs.microsoft.com/windows-hardware/drivers/kernel/porting-your-driver-to-64-bit-windows)中的64位移植指导原则。 本主题介绍编写64位打印机驱动程序时可能遇到的一些限制和问题。

有关使用修饰来识别64位体系结构的详细信息，请参阅以下主题：

- [打印机 INF 文件中的修饰](decorations-in-printer-inf-files.md)

- [如何使用打印机驱动程序 INF 文件中的修饰](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

## <a name="limitations-on-device-context-handles"></a>设备上下文句柄的限制

如果32位应用程序正在64位版本的 Microsoft Windows 操作系统上运行，则在 Splwow64.exe thunk 进程的上下文中运行的打印机驱动程序插件不应调用 GDI **CreateDC** 函数;此调用将失败。

## <a name="problems-with-writing-64-bit-drivers"></a>编写64位驱动程序时遇到的问题

在现有的32位驱动程序代码中，请注意指针类型和整数类型（如 DWORD 或 ULONG）之间的转换。 如果你有为32位计算机编写代码的经验，则可以使用来假定指针值适合 DWORD 值或 ULONG。 对于64位代码，此假设是危险的。 如果将指针转换为类型 DWORD 或 ULONG，则可能会截断64位指针。

相反，将指针强制转换为类型 DWORD \_ ptr 或 ULONG \_ ptr。 类型为 DWORD \_ ptr 或 ULONG ptr 的无符号整数 \_ 始终足够大以存储整个指针，无论代码是针对32位计算机还是64位计算机编译的。

例如， [**OEMCUIPPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam) 结构中的 pDrvOptItems 指针字段的类型为 ULONG \_ PTR。 下面的代码示例演示了将64位指针值复制到此字段时不会执行的操作。

```cpp
PUSERDATA pData;
OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG)pData;  // Wrong
```

前面的代码示例将 *pData* 指针转换为类型 ULONG，如果 **sizeof** (*PDATA*) > **sizeof** (ULONG) ，则会截断指针值。 正确的方法是将指针转换为 ULONG \_ PTR，如下面的代码示例中所示。

```cpp
PUSERDATA pData;
OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG_PTR)pData;  // Correct
```

前面的代码示例保留指针值的所有64位。

内联64位函数（如 **PtrToUlong** 和 **UlongToPtr** ）在指针和整数类型之间安全转换，而不依赖于这些类型的相对大小假设。 如果一种类型的长度较短，则必须在转换为较长的类型时进行扩展。 如果通过使用符号位或零填充来扩展较短的类型，则每个 Win64 函数都可以处理这些情况。 请考虑以下代码示例。

```cpp
ULONG ulHWPhysAddr[NUM_PHYS_ADDRS];
ulSlotPhysAddr[0] = ULONG(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // wrong
```

应将上面的代码示例替换为下面的代码示例。

```cpp
ULONG_PTR ulHWPhysAddr[NUM_PHYS_ADDRS];
ulSlotPhysAddr[0] = PtrToUlong(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // correct
```

第二个代码示例是首选的，即使

```cpp
ulSlotPhysAddr
```

可能表示仅32位长而不是64位的硬件寄存器的值。 有关在指针和整数类型之间进行转换的所有新的 Win64 helper 函数的列表，请参阅 [新的数据类型](https://docs.microsoft.com/windows-hardware/drivers/kernel/the-new-data-types)。
