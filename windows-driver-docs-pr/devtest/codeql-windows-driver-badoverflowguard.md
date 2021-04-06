---
title: 'BadOverflowGuard (补充 Windows 驱动程序 CodeQL 查询) '
description: BadOverflowGuard 补充 Windows Driver CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: 9b71af7f2a241f0985565de40abf0ad4392e661a
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106387620"
---
# <a name="badoverflowguard-windows-driver-codeql-query"></a>BadOverflowGuard (Windows Driver CodeQL Query) 

## <a name="overview"></a>概述

如果所有参数类型的大小小于4个字节，则检查添加的某个参数是否溢出会失败。 这是因为添加的结果被提升为4字节 int。

## <a name="recommendation"></a>建议

通过将加法与至少为4个字节的值进行比较来检查溢出。

## <a name="example"></a>示例

在此示例中，比较结果将导致整数溢出：

```cpp
unsigned short CheckForInt16OverflowBadCode(unsigned short v, unsigned short b)
{
    if (v + b < v) // BUG: "v + b" will be promoted to 32 bits
    {
        // ... do something
    }
    return v + b;
}
```

若要修复此错误，请通过将加法与至少为4个字节的值进行比较来检查溢出：

```cpp
unsigned short CheckForInt16OverflowCorrectCode(unsigned short v, unsigned short b)
{
    if (v + b > 0x00FFFF)
    {
        // ... do something
    }
    return v + b;
}
```

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。
