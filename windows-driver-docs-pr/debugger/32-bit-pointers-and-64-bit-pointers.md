---
title: 32 位指针和 64 位指针
description: 32 位指针和 64 位指针
ms.assetid: 641443b9-465f-4c7e-a13d-47a991304b46
keywords:
- WdbgExts 扩展，32 位指针
- WdbgExts 扩展，64 位指针
ms.date: 11/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 05a584cc956664402ec18ff9cf2de05f406fc8c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567309"
---
# <a name="32-bit-pointers-and-64-bit-pointers"></a>32 位指针和 64 位指针


## <span id="ddk_32_bit_pointers_and_64_bit_pointers_dbwx"></span><span id="DDK_32_BIT_POINTERS_AND_64_BIT_POINTERS_DBWX"></span>


WdbgExts.h 标头文件支持 32 位和 64 位指针。 若要使用 64 位指针，只需在代码中，按以下顺序包含以下两行：

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
```

建议在代码中始终使用 64 位指针。 因为调试器将自动转换到 32 位的 64 位指针目标为 32 位，这允许你在任何平台上工作的扩展。

如果你想要仅在 32 位平台上使用你的扩展，可以改为编写的 32 位扩展。 在这种情况下，只需在代码中包含以下行：

```cpp
#include wdbgexts.h 
```
使用 64 位指针的其他信息，请参阅[使用 DECLARE_API 宏](using-the-declare-api-macro.md)并[编写 WdbgExts 扩展代码](writing-wdbgexts-extension-code.md)。 此外，检查是 WDK 的一部分包含的示例代码。



 

 





