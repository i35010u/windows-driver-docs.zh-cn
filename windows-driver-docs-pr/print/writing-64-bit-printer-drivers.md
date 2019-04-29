---
title: 写 64 位打印机驱动程序
description: 写 64 位打印机驱动程序
ms.assetid: 41f1a521-980e-4ccd-a395-e1d1bf0114d1
keywords:
- 打印机驱动程序 WDK，64 位
- 64 位 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a1c36223634ad720723c11b20cecbde29f3a2fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370361"
---
# <a name="writing-64-bit-printer-drivers"></a>写 64 位打印机驱动程序


如果要编写的 64 位驱动程序或编写可编译为 32 位和 64 位系统上运行的驱动程序，请按照中的 64 位迁移指导原则[驱动程序的编程技术](https://msdn.microsoft.com/library/windows/hardware/ff554452)。 本主题介绍了一些限制和编写的 64 位打印机驱动程序可能会遇到的问题。

有关使用修饰确定 64 位体系结构的详细信息，请参阅以下主题：

-   [打印机 INF 文件中的修饰](decorations-in-printer-inf-files.md)

-   [如何将使用的打印机驱动程序的 INF 文件中的修饰](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

### <a name="limitations-on-device-context-handles"></a>设备上下文句柄的限制

如果在 64 位版本的 Microsoft Windows 操作系统上运行的 32 位应用程序的打印机驱动程序插件 Splwow64.exe 形式转换过程的上下文中运行不应调用 GDI **CreateDC**函数;此调用将失败。

### <a name="problems-with-writing-64-bit-drivers"></a>编写 64 位驱动程序的问题

在现有的 32 位驱动程序代码中，要格外小心指针类型和如 DWORD 或 ULONG 的整数类型之间的转换。 如果已为在 32 位计算机编写代码的体验，则可能使用到这是假定适合 DWORD 或 ULONG 的指针值。 对于 64 位代码，这一假设是危险的。 如果将转换为指向类型 DWORD 或 ULONG 的指针，64 位指针可能被截断。

相反，强制转换指针类型 DWORD\_PTR 或 ULONG\_PTR。 无符号的整数的类型为 DWORD\_PTR 或 ULONG\_PTR 始终有足够空间来存储整个指针，而不考虑是否会将代码编译为 32 位或 64 位计算机。

例如，pDrvOptItems.UserData 指针中的字段[ **OEMCUIPPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff557653)结构是类型为 ULONG\_PTR。 下面的代码示例显示了要不执行的操作如果将一个 64 位指针值复制到此字段。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG)pData;  // Wrong
```

前面的代码示例强制转换*pData*指向类型 ULONG，如果可以截断该指针值的指针**sizeof**(*pData*) &gt; **sizeof**(ULONG)。 正确的方法是将强制转换为 ULONG 的指针\_PTR，如下面的代码示例中所示。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG_PTR)pData;  // Correct
```

前面的代码示例将保留所有 64 位指针值。

内联 64-bit 之类的函数**PtrToUlong**并**UlongToPtr**安全地指针和整数类型之间转换而不依赖于这些类型的相对大小假设。 如果短于另一种类型，必须将转换为时间类型时扩展。 如果在较短类型可通过使用符号位或用零填充进行扩展，每个 Win64 函数可以处理这些情况。 请考虑下面的代码示例。

```cpp
    ULONG ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // wrong
```

下面的代码示例中应替换前面的代码示例。

```cpp
    ULONG_PTR ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // correct
```

即使是首选的第二个代码示例

```cpp
ulSlotPhysAddr
```

可能表示仅 32 位长而不是 64 位长硬件寄存器的值。 所有新 Win64 帮助程序函数的指针和整数类型之间进行转换的列表，请参阅[新的数据类型](https://msdn.microsoft.com/library/windows/hardware/ff564619)。
 

 




