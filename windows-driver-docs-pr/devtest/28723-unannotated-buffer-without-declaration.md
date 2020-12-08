---
title: C28723
description: 警告 C28723 函数定义中没有相应声明的批注缓冲区。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28723
ms.openlocfilehash: 9368d7479f4d8093fa5a9a9a44dc0587cd6888a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841355"
---
# <a name="c28723"></a>C28723


警告 C28723：在函数定义中没有相应声明的批注缓冲区

此警告表明，作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可使用此类注释来检测缓冲区溢出。

目前，此警告只诊断了非常量的缓冲区。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码示例将生成此警告。

```
    int foo( LPTSTR buffer, size_t cch )
{
    ...
}  
```

下面的代码示例可避免此警告。

```
    int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch )
{
    ...
}
```









