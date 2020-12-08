---
title: C30034
description: 警告 C30034 将标志值传递给可能导致分配可执行内存的分配函数。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30034
ms.openlocfilehash: 616bfdb6f2042be0a7fc4c495d236d061fcac6e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813885"
---
# <a name="c30034"></a>C30034


警告 C30034：将标志值传递给可能导致分配可执行内存的分配函数。 请验证分配函数未请求可执行的非分页池的形式。

禁止的 \_ 内存 \_ 分配 \_ 可能 \_ 不安全

调用了对函数的调用，导致可执行的可执行非分页池分配。 使用的参数指示生成的分配实际上可能是不可执行的，但确定这不太可能是因为分配了可执行的内存。 最常见的情况是，使用将可选的分配函数作为参数的函数。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码将生成此警告，因为在 *pAllocate* 中分配指定的类型时，它是未知的，这是第四个参数 (0，这是可执行) ，或者从 pAllocate 内设置分配类型 *。*

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

 

 





