---
title: 导入内核模式安全字符串函数
description: 导入内核模式安全字符串函数
keywords:
- 导入安全字符串函数
- 内联安全字符串函数版本 WDK 内核
- 库安全字符串函数版本 WDK 内核
- 字节计数函数 WDK 内核
- 字符计数函数 WDK 内核
- 安全字符串函数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a015748fb39100819c36ed7d53dd8e5cb4161853
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788659"
---
# <a name="importing-kernel-mode-safe-string-functions"></a>导入内核模式安全字符串函数





从 Windows XP 开始，内核模式安全字符串库可用作在 Ntstrsafe.h 而头文件中定义的内联函数的集合。

### <a name="to-use-the-kernel-mode-safe-string-functions"></a><a href="" id="to-use-the-inline-versions-of-the-kernel-mode--safe-string-functions"></a>使用内核模式安全字符串函数

包括头文件，如下所示。

```cpp
#include <ntstrsafe.h>
```

你可以仅对字节计数或仅限字符计数的安全字符串函数提供。

### <a name="to-allow-only-byte-counted-functions"></a>仅允许字节计数的函数

在包含 Ntstrsafe.h 而头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_CCH_FUNCTIONS
```

### <a name="to-allow-only-character-counted-functions"></a>仅允许字符计数函数

在包含 Ntstrsafe.h 而头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_CB_FUNCTIONS
```

你可以定义 NTSTRSAFE.H 而 \_ \_ \_ 或 Ntstrsafe.h 而 \_ no \_ CCH \_ 函数，但不能同时定义这两者。

您可以使 [**UNICODE \_ 字符串**](/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构函数不可用。

### <a name="to-make-unicode_string-structure-functions-unavailable"></a><a href="" id="to-make-unicode-string-structure-functions-unavailable"></a>使 UNICODE \_ 字符串结构函数不可用

在包含 Ntstrsafe.h 而头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_UNICODE_STRING_FUNCTIONS
```

任何 ANSI 或 Unicode 字符串可包含的最大字符数为 NTSTRSAFE.H 而 \_ MAX \_ CCH。 **Unicode \_ 字符串** 结构可包含的最大字符数为 Ntstrsafe.h 而 \_ unicode \_ string \_ MAX \_ CCH。 这些常量在 Ntstrsafe.h 而中定义。

通过在代码中包含以下行，你的驱动程序可以 \_ \_ \_ \_ \_ \_ 通过在代码中包含以下行，将较小的值分配给 Ntstrsafe.h 而 max CCH 和 ntstrsafe.h 而 UNICODE STRING MAX CCH。

```cpp
#define NTSTRSAFE_MAX_CCH  <new-value>
#define NTSTRSAFE_UNICODE_STRING_MAX_CCH  <new-value>
```

Ntstrsafe.h 而中的指令验证新值是否不大于默认值。

 

