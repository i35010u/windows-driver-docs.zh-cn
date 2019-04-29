---
title: C28722
description: 警告 C28722 未批注缓冲区函数声明中。
ms.assetid: 460B9F71-9878-4DC8-8B93-6DCDF1544213
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28722
ms.openlocfilehash: 8624b4e1ed7e5b72714864546d4fcf9aa99c2ae2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363861"
---
# <a name="c28722"></a>C28722


警告 C28722:函数声明中的一个未批注的缓冲区

此警告指示作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可使用此类批注来检测在编译时缓冲区溢出。

目前，仅非常量缓冲区诊断并发出以下警告。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码示例将生成此警告。

```CSS
int foo( LPTSTR buffer, size_t cch );  
```

下面的代码示例使用 SAL 批注，因此可避免此警告**\_出\_写入\_** 指定所调用的函数将写入缓冲区和缓冲区不能为 NULL。 该批注指示缓冲区是否属于*cch*元素。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





