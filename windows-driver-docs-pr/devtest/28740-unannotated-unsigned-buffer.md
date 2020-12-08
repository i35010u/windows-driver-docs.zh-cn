---
title: C28740
description: 警告 C28740 批注无符号缓冲区。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28740
ms.openlocfilehash: f81d790abd38be2f7a4fb1365e5173a3da6fcdd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803979"
---
# <a name="c28740"></a>C28740


警告 C28740：批注无符号缓冲区

此警告表明，作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可使用此类注释来检测缓冲区溢出。

目前，此警告只诊断了非常量的缓冲区。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码示例将生成此警告。

```
    int foo( BYTE * buffer, size_t cch ); 
```

下面的代码示例通过使用 SAL 注释 **\_ Out \_ 写入 \_** 来指定被调用函数写入缓冲区并且缓冲区不能为 NULL，从而避免出现此警告。 批注指示缓冲区是 *cch* 元素。

```
    int foo( _Out_writes_(cch) BYTE * buffer, size_t cch );
```

 

 





