---
title: WDI TLV 生成器/分析器内存接口
description: 分析器和生成器在内部将 c + + 与 new/delete 一起使用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498e0f2fcfd299d336f082b5896c20e14a88a3c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837879"
---
# <a name="wdi-tlv-generatorparser-memory-interface"></a>WDI TLV 生成器/分析器内存接口


分析器和生成器在内部将 c + + 与 new/delete 一起使用。 这简化了若干实现细节。 这意味着库的使用者必须在链接到库时提供这些 Api 的重载运算符实现。 这是代码必须采用的唯一 c + + 依赖项。

所有执行分配的 Api 都采用类型为 PCTLV 的参数 *上下文* ， \_ 该上下文具有2个字段：一个 \_ 名为 **AllocationContext** 的 Ulong PTR 和一个名为 **PeerVersion** 的 ulong。 将 **AllocationContext** 字段传递到重载 `new` 运算符。 这允许 Api 的使用者以不同的方式自定义分配。 有关 TLV 上下文参数的详细信息 \_ ，请参阅 [WDI TLV 版本控制](wdi-tlv-versioning.md)。

**警告**  尽管你可能会尝试跳过调用库的清理例程 (例如 FreeParsed、CleanupParsed 和 FreeGenerated) ，但不要跳过调用它们！ 它可能适用于一些代码路径，但会导致难以诊断的内存泄漏。

 

下面是一个示例重载运算符。

```C++
/*++
Module Name:
    sample.cpp
Abstract:
    Contains sample code to override C++ new/delete for use with TLV parser/generator library
Environment:
    Kernel mode
--*/
#include "precomp.h"

#define TLV_POOL_TAG (ULONG) '_VLT'

void* __cdecl operator new(size_t Size, ULONG_PTR AllocationContext)
/*++
  Override C++ allocation operator.
--*/
{
    PVOID pData = ExAllocatePoolWithTag(NonPagedPoolNx, Size, TLV_POOL_TAG);
    UNREFERENCED_PARAMETER(AllocationContext);
    if (pData != NULL)
    {
        RtlZeroMemory( pData, Size);
    }
    return pData;
} 

void __cdecl operator delete(void* pData)
/*++
  Override C++ delete operator.
--*/
{
    if (pData != NULL)
    {
        ExFreePoolWithTag(pData, TLV_POOL_TAG);
    }
}
```

 

 





