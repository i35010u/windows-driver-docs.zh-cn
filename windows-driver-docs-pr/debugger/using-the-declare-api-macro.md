---
title: 使用 DECLARE_API 宏
description: 使用 DECLARE_API 宏
keywords:
- WdbgExts 扩展，DECLARE_API 宏
- 'DECLARE_API 宏 (WdbgExts) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc6c55825b7befb6aeb81ad748e95140b71a8fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803027"
---
# <a name="using-the-declare_api-macro"></a>使用 DECLARE \_ API 宏


## <span id="ddk_using_the_declare_api_macro_dbwx"></span><span id="DDK_USING_THE_DECLARE_API_MACRO_DBWX"></span>


WdbgExts 扩展 DLL 中的每个扩展命令都是使用 DECLARE \_ API 宏声明的。 此宏是在 wdbgexts 中定义的。

扩展命令的代码的基本格式为：

```cpp
DECLARE_API( myextension )
{
    code for myextension
}
```

DECLARE \_ API 宏为扩展命令设置标准接口。 例如，如果用户将任何自变量传递给 extension 命令，则整个参数字符串将存储为字符串，并将指向此字符串)  (的指针作为 **参数** 传递给扩展函数。

如果使用的是64位指针，则按 \_ 如下方式定义 DECLARE API 宏：

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

如果你使用的是32位指针，则声明 \_ API 保持不变，只不过 **dwCurrentPc** 将为 ULONG 类型而不是 ULONG64。 但是，建议为正在编写的任何扩展名使用64位指针。 有关详细信息，请参阅 [32 位指针和64位指针](32-bit-pointers-and-64-bit-pointers.md) 。

 

 





