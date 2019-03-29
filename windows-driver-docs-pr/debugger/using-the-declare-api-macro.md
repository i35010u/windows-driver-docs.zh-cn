---
title: 使用 DECLARE_API 宏
description: 使用 DECLARE_API 宏
ms.assetid: 469f5ae4-2da8-4bbe-b5c0-75fcef227ba5
keywords:
- WdbgExts 扩展，DECLARE_API 宏
- DECLARE_API 宏 (WdbgExts)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bef24f2a95008024f023fb1f89fa18f4b8ffffd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563067"
---
# <a name="using-the-declareapi-macro"></a>使用 DECLARE\_API 宏


## <span id="ddk_using_the_declare_api_macro_dbwx"></span><span id="DDK_USING_THE_DECLARE_API_MACRO_DBWX"></span>


使用 DECLARE 声明 WdbgExts 扩展 DLL 中的每个扩展命令\_API 宏。 Wdbgexts.h 中定义此宏。

扩展命令的代码的基本格式为：

```cpp
DECLARE_API( myextension )
{
    code for myextension
}
```

DECLARE\_API 宏设置扩展命令的标准接口。 例如，如果用户向扩展命令传递任何自变量，会将整个参数字符串存储为字符串，并指向此字符串 (作为 PCSTR) 的指针将传递给扩展函数作为**args**。

如果您使用的 64 位指针，DECLARE\_API 宏的定义如下：

```cpp
#define DECLARE_API(s)                             \
    CPPMOD VOID                                    \
    s(                                             \
        HANDLE                 hCurrentProcess,    \
        HANDLE                 hCurrentThread,     \
        ULONG64                dwCurrentPc,        \
        ULONG                  dwProcessor,        \
        PCSTR                  args                \
     )
```

如果您使用的 32 位指针，DECLARE\_API 将保持不变，不同之处在于**dwCurrentPc**的类型而不是 ULONG64 ULONG 将为。 但是，64 位指针建议对于任何扩展写入。 请参阅[32 位指针和 64 位指针](32-bit-pointers-and-64-bit-pointers.md)有关详细信息。

 

 





