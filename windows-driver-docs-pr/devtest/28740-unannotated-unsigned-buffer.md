---
title: C28740
description: 警告 C28740 未批注的无符号的缓冲区。
ms.assetid: 849BA4E4-89E7-4E8C-B73C-CA303487A5E3
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28740
ms.openlocfilehash: 83530c43b283d4e54291c01f7e98ba89d536be66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374741"
---
# <a name="c28740"></a>C28740


警告 C28740:一个未批注的无符号的缓冲区

此警告指示作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可以使用此类批注检测缓冲区溢出。

目前，仅非常量缓冲区诊断并发出以下警告。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码示例将生成此警告。

```
    int foo( BYTE * buffer, size_t cch ); 
```

下面的代码示例使用 SAL 批注，因此可避免此警告**\_出\_写入\_** 指定所调用的函数将写入缓冲区和缓冲区不能为 NULL。 该批注指示缓冲区是否属于*cch*元素。

```
    int foo( _Out_writes_(cch) BYTE * buffer, size_t cch );
```

 

 





