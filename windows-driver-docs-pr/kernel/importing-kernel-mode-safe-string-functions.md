---
title: 导入内核模式安全字符串函数
description: 导入内核模式安全字符串函数
ms.assetid: f1cee7e0-151b-4e03-bf4d-400f328083fa
keywords:
- 导入安全字符串函数
- 内联安全字符串函数版本 WDK 内核
- 库安全字符串函数版本 WDK 内核
- 字节计数函数 WDK 内核
- 字符计数函数 WDK 内核
- 安全字符串函数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb386f4c92bbcc2133be9ca330464af2d4547c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828307"
---
# <a name="importing-kernel-mode-safe-string-functions"></a>导入内核模式安全字符串函数





从 Windows XP 开始，内核模式安全字符串库可用作在 Ntstrsafe.h 而头文件中定义的内联函数的集合。

### <a href="" id="to-use-the-inline-versions-of-the-kernel-mode--safe-string-functions"></a>使用内核模式安全字符串函数

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

可以定义 NTSTRSAFE.H 而\_NO\_CB\_函数或 NTSTRSAFE.H 而\_无\_CCH\_函数，但不能同时定义两者。

您可以使[**UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)结构函数不可用。

### <a href="" id="to-make-unicode-string-structure-functions-unavailable"></a>使 UNICODE\_字符串结构函数不可用

在包含 Ntstrsafe.h 而头文件之前，请在代码中包含以下行。

```cpp
#define NTSTRSAFE_NO_UNICODE_STRING_FUNCTIONS
```

任何 ANSI 或 Unicode 字符串可包含的最大字符数都是 NTSTRSAFE.H 而\_MAX\_CCH。 **Unicode\_字符串**结构可包含的最大字符数\_UNICODE\_STRING\_MAX\_CCH。 这些常量在 Ntstrsafe.h 而中定义。

通过在代码中包含以下行，你的驱动程序可以通过在代码中包含以下行，将较小的值分配给 NTSTRSAFE.H 而\_最大\_CCH 和 NTSTRSAFE.H 而\_UNICODE\_字符串\_

```cpp
#define NTSTRSAFE_MAX_CCH  <new-value>
#define NTSTRSAFE_UNICODE_STRING_MAX_CCH  <new-value>
```

Ntstrsafe.h 而中的指令验证新值是否不大于默认值。

 

 




