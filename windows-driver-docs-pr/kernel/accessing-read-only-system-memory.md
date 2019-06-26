---
title: 访问只读的系统内存
description: 访问只读的系统内存
ms.assetid: d2c1f933-3a7e-4e82-b96d-4f019b27abd5
keywords:
- 内存管理 WDK 内核，只读内存
- 只读存储器 WDK 内核
- 截获系统调用
- 全局字符串 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84683f22535a2f04dd2eeb6c3771f7e00a0dbccd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382268"
---
# <a name="accessing-read-only-system-memory"></a>访问只读的系统内存





Windows[内存管理器](windows-kernel-mode-memory-manager.md)强制执行的页的未标记为可写的只读访问。

始终在用户模式下保护只读内存。 但是，在 Windows NT 4.0 和更早版本中，只读内存不受保护在内核模式下。

如果 Windows 内核模式驱动程序或应用程序尝试写入只读内存段，系统会发出错误检查。 有关详细信息，请参阅[ **Bug 检查 0xBE:尝试\_编写\_TO\_READONLY\_内存**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xbe--attempted-write-to-readonly-memory)。

### <a name="intercepting-system-calls"></a>截获系统调用

某些驱动程序截距系统调用通过覆盖驱动程序自己的代码并将插入跳转的说明或进行其他更改。 驱动程序自己的代码是只读的因为此方法将导致要颁发的 bug 检查。

### <a name="global-strings"></a>全局字符串

如果要修改的全局字符串，则它必须不能声明为指向常量值的指针：

```cpp
CHAR *myString = "This string cannot be modified.";
```

在这种情况下，链接器可能会将字符串放在只读内存段中。 然后尝试修改该字符串将导致的 bug 检查。

相反，该字符串应显式声明为左值的字符数组：

```cpp
CHAR myString[] = "This string can be modified.";
```

此声明可确保字符串置于可写内存。

 

 




