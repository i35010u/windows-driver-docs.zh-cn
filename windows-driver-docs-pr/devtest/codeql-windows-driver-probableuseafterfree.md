---
title: 'ProbableUseAfterFree (补充 Windows 驱动程序 CodeQL 查询) '
description: UseAfterFree，低精度 a 补充 Windows 驱动程序 CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: 2d513f37f8fffddcbb405009a7011d95d3cd4fe6
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648164"
---
# <a name="probable-useafterfree-windows-driver-codeql-query"></a>可能的 UseAfterFree（Windows 驱动程序 CodeQL 查询）

## <a name="overview"></a>概述

此 [CodeQL 查询](./static-tools-and-codeql.md) 的精度低于高精度 [UseAfterFree](./codeql-windows-driver-useafterfree.md) CodeQL 查询。 它检测到一些其他方案，但也有更高的误报速率。

如果在释放分配的内存块 (也称为 "无关联指针" ) ，则会发生 [UseAfterFree 缺陷](http://cwe.mitre.org/data/definitions/416.html) 。

此类情况下的行为是未定义的，并且实际上可能会产生意想不到的后果，其中包括内存损坏、使用错误值或执行任意代码。

## <a name="recommendation"></a>建议

释放指针后立即将其设置为 NULL。

## <a name="example"></a>示例
在下面的示例中， `pSomePointer` 仅当 `Status` 值不为零，且在取消引用之前，才会释放，然后 `pSomePointer` `Method` `Status` 再次选中。  遗憾 `Status` 的是，在对的两个引用之间进行了更改 `pSomePointer` ，这允许问题 `pSomePointer->Method()` 通过以前释放的指针执行对的调用。

```c
NTSTATUS Status = x();

if (Status != 0)
{
    // Release pSomePointer if the call to x() failed

    ExFreePool(pSomePointer);
}

Status = y();

if (Status == 0)
{
    // Because Status may no longer be the same value than it was before the pointer was released,
    // this code may be using pSomePointer after it was freed, potentially executing arbitrary code.

    Status = pSomePointer->Method();
}
```
在更正后的示例中，将 `pSomePointer` 设置为在 `NULL` 释放后立即设置为，并检查是否可以安全调用 `pSomePointer->Method()` 此附加条件的检查以防止可能的 bug。


```c
NTSTATUS Status = x();

if (Status != 0)
{
    // Release pSomePointer if the call to x() failed

    ExFreePool(pSomePointer);

    // Setting pSomePointer to NULL after being freed
    pSomePointer = NULL;
}

Status = y();

// If pSomePointer was freed above, its value must have been set to NULL
if (Status == 0 && pSomePointer != NULL)
{
    Status = pSomePointer->Method();
}
```

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。