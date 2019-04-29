---
title: WDI TLV 生成器/分析器内存接口
description: 分析器和生成器在内部使用C++new/delete。
ms.assetid: 318519FF-AF1F-4D86-96A9-ED0918D91310
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50a22edbd4e4ee495ea517e82dcdf0255f01a95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382860"
---
# <a name="wdi-tlv-generatorparser-memory-interface"></a>WDI TLV 生成器/分析器内存接口


分析器和生成器在内部使用C++new/delete。 这简化了多个实现详细信息。 这意味着时链接到此库，库的使用者必须提供这些 Api 的重载的运算符实现。 这是唯一C++你的代码必须执行的依赖关系。

执行任何分配的所有 Api 都采用参数*上下文*PCTLV 类型化为\_上下文，其中包括 2 个字段： ULONG\_名为 PTR **AllocationContext**和名为ULONG**PeerVersion**。 **AllocationContext**字段传递到重载`new`运算符。 这允许使用者的自定义以各种方式分配的 Api。 详细了解 TLV\_上下文参数，请参阅[WDI TLV 版本控制](wdi-tlv-versioning.md)。

**警告**  尽管您可能想要跳过调用库的清理例程 （例如 FreeParsed、 CleanupParsed 和 FreeGenerated），请勿跳过调用它们 ！ 它可能适用于某些代码路径，但将导致与硬诊断内存泄漏。

 

下面是示例重载运算符。

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

 

 





