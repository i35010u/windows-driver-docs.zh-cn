---
title: 访问只读的系统内存
description: 访问只读的系统内存
ms.assetid: d2c1f933-3a7e-4e82-b96d-4f019b27abd5
keywords:
- 内存管理 WDK 内核，只读内存
- 只读内存 WDK 内核
- 截获系统调用
- 全局字符串 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6d2fd7e0d6f30697410c3267b8a42f8a6e688d9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189094"
---
# <a name="accessing-read-only-system-memory"></a>访问只读的系统内存





Windows [内存管理器](windows-kernel-mode-memory-manager.md) 强制对未标记为可写的页进行只读访问。

只读内存始终在用户模式下受到保护。 但是，在 Windows NT 4.0 及更早版本中，只读内存在内核模式下不受保护。

如果 Windows 内核模式驱动程序或应用程序尝试写入只读内存段，系统会发出 bug 检查。 有关详细信息，请参阅 [**Bug 检查0xBE： \_ 尝试 \_ 写入 \_ 只读 \_ 内存**](../debugger/bug-check-0xbe--attempted-write-to-readonly-memory.md)。

### <a name="intercepting-system-calls"></a>截获系统调用

某些驱动程序通过覆盖驱动程序自己的代码，并插入跳转指令或其他更改来截获系统调用。 由于驱动程序自己的代码是只读的，因此此方法会导致发出 bug 检查。

### <a name="global-strings"></a>全局字符串

如果要修改全局字符串，则不能将其声明为指向常量值的指针：

```cpp
CHAR *myString = "This string cannot be modified.";
```

在这种情况下，链接器可能会将字符串置于只读内存段中。 然后，尝试修改该字符串将导致 bug 检查。

相反，应将该字符串显式声明为左值字符的数组：

```cpp
CHAR myString[] = "This string can be modified.";
```

此声明可确保将该字符串放入可写内存。

 

