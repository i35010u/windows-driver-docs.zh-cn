---
title: 32 位指针和 64 位指针
description: 32 位指针和 64 位指针
keywords:
- WdbgExts 扩展，32位指针
- WdbgExts 扩展，64位指针
ms.date: 11/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5af8699f8eb354a668ef6456006374e9a07dfcb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819335"
---
# <a name="32-bit-pointers-and-64-bit-pointers"></a>32 位指针和 64 位指针


## <span id="ddk_32_bit_pointers_and_64_bit_pointers_dbwx"></span><span id="DDK_32_BIT_POINTERS_AND_64_BIT_POINTERS_DBWX"></span>


WdbgExts 头文件支持32位和64位指针。 若要使用64位指针，只需在代码中包含以下两行代码，顺序如下：

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
```

建议在代码中始终使用64位指针。 这允许你的扩展在任何平台上工作，因为当目标为32位时，调试器会自动将64位指针转换为32位。

如果你只想在32位平台上使用你的扩展，则可以改为编写32位扩展。 在这种情况下，你只需在代码中包含以下行：

```cpp
#include wdbgexts.h 
```
有关使用64位指针的其他信息，请参阅 [使用 DECLARE_API 宏](using-the-declare-api-macro.md) 和 [编写 WdbgExts 扩展代码](writing-wdbgexts-extension-code.md)。 此外，请检查作为 WDK 一部分包含的示例代码。



 

 





