---
title: C28723
description: 警告 C28723 未批注缓冲区中有没有相应的声明的函数定义。
ms.assetid: FE481A48-F4C1-4C25-8CE6-3802D57B8F68
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28723
ms.openlocfilehash: 00ab9831c34b4aed7f7ec81c31fa67cdab60402a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323825"
---
# <a name="c28723"></a>C28723


警告 C28723:有没有相应的声明的函数定义中的一个未批注的缓冲区

此警告指示作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可以使用此类批注检测缓冲区溢出。

目前，仅非常量缓冲区诊断并发出以下警告。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


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









