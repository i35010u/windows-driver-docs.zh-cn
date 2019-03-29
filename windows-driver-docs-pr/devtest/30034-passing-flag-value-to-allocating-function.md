---
title: C30034
description: 警告 C30034 传递到可能会导致可执行文件所分配的内存的分配函数的标志值。
ms.assetid: 11B06B23-17B4-4B97-A1EE-3351B72B7B1D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30034
ms.openlocfilehash: dded5285c83771be4df8fc3b2402aa4d50a570ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576029"
---
# <a name="c30034"></a>C30034


警告 C30034:传递给可能会导致可执行文件所分配的内存分配函数的标志值。 请验证正在分配的函数不请求一种形式的可执行文件的非分页缓冲池。

已禁止\_内存优化\_分配\_也许\_UNSAFE

已找到的可执行文件的非分页缓冲池可能是因为分配会导致一个函数调用。 使用参数指示产生的分配实际上可能是不可执行，但确定这是不可能和可执行文件的内存已分配。 这是最常见的使用可选的分配函数作为参数的函数。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码生成此警告，因为如果不知道*pAllocate*分配指定的类型-在此第四个参数 (0，这是可执行文件) 或分配类型集内*pAllocate。*

```
ExInitializeNPagedLookasideList(   pLookaside,
                pAllocate,
                pFree,
                0,
                size,
                tag,
                depth);
```

下面的代码可避免此警告：

```
ExInitializeNPagedLookasideList(   pLookaside,
                pAllocate,
                pFree,
                POOL_NX_ALLOCATION,
                size,
                tag,
                depth);
```

 

 





