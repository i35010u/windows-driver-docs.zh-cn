---
title: 'InfiniteLoop (补充 Windows 驱动程序 CodeQL 查询) '
description: InfiniteLoop 补充 Windows Driver CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: 85d56b3f001b44fce6d1de8cfab13131507e1745
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106387622"
---
# <a name="infiniteloop-windows-driver-codeql-query"></a>InfiniteLoop (Windows Driver CodeQL Query) 

## <a name="overview"></a>概述

循环条件中不同宽度的类型之间的比较可能会导致循环无法终止。

## <a name="recommendation"></a>建议

在循环条件中使用适当的类型。

## <a name="example"></a>示例

在此示例中，如果参数的值大于 *SHRT_MAX*，则比较结果可能导致无限 *循环：*

```cpp
void InfiniteLoop(int a)
{
    for (short i = 0; i < a; i++) // BUG: infinite loop
    {
        // ...
    }
}
```

若要修复此 bug，我们要更改变量 *i* *与的宽度* 匹配的类型：

```cpp
void NotInfiniteLoop(int a)
{
    for (int i = 0; i < a; i++) 
    {
        // ...
    }
}
```

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。
