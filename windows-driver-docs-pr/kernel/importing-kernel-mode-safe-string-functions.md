---
title: 导入内核模式安全字符串函数
description: 导入内核模式安全字符串函数
ms.assetid: f1cee7e0-151b-4e03-bf4d-400f328083fa
keywords:
- 导入安全的字符串函数
- 内联安全的字符串函数版本 WDK 内核
- 库安全的字符串函数版本 WDK 内核
- 字节计数函数 WDK 内核
- 字符计数函数 WDK 内核
- 安全字符串函数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aeddeea0d159ece37d624c28af2966ca1c4fb0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369799"
---
# <a name="importing-kernel-mode-safe-string-functions"></a>导入内核模式安全字符串函数





从 Windows XP，内核模式安全字符串库是可用作 Ntstrsafe.h 标头文件中定义的内联函数的集合。

### <a href="" id="to-use-the-inline-versions-of-the-kernel-mode--safe-string-functions"></a>若要使用的内核模式安全字符串函数

包括标头文件，如所示。

```cpp
#include <ntstrsafe.h>
```

您可以提供仅字节计数或仅字符被安全的字符串函数。

### <a name="to-allow-only-byte-counted-functions"></a>若要允许仅字节计数函数

在包含 Ntstrsafe.h 标头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_CCH_FUNCTIONS
```

### <a name="to-allow-only-character-counted-functions"></a>若要允许仅字符计函数

在包含 Ntstrsafe.h 标头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_CB_FUNCTIONS
```

可以定义任一 NTSTRSAFE\_否\_CB\_函数或 NTSTRSAFE\_否\_CCH\_函数，但不可同时使用两者。

可以使[ **UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)结构函数不可用。

### <a href="" id="to-make-unicode-string-structure-functions-unavailable"></a>若要使 UNICODE\_字符串结构函数不可用

在包含 Ntstrsafe.h 标头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_UNICODE_STRING_FUNCTIONS
```

最大的任何 ANSI 或 Unicode 字符串可以包含的字符数是 NTSTRSAFE\_最大\_CCH。 最大字符数的**UNICODE\_字符串**结构可以包含为 NTSTRSAFE\_UNICODE\_字符串\_最大\_CCH。 这些常量 Ntstrsafe.h 中定义。

您的驱动程序可以将较小的值分配给 NTSTRSAFE\_最大\_CCH 和 NTSTRSAFE\_UNICODE\_字符串\_最大\_CCH 通过之前包括在代码中包含以下行Ntstrsafe.h。

```cpp
#define NTSTRSAFE_MAX_CCH  <new-value>
#define NTSTRSAFE_UNICODE_STRING_MAX_CCH  <new-value>
```

指令 Ntstrsafe.h 中的验证你的新值不是大于默认值。

 

 




