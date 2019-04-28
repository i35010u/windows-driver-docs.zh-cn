---
title: C28718
description: 警告 C28718 未批注的缓冲区。
ms.assetid: 8417AB73-B645-451D-A359-9A66A793A78D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28718
ms.openlocfilehash: cd4afb516ac9df4d2d9a92116f59c3569ae3c5cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345851"
---
# <a name="c28718"></a>C28718


警告 C28718:一个未批注的缓冲区

传递给函数或函数返回的缓冲区不包含源代码批注语言 (SAL) 注释时，将报告此警告。 静态分析工具可以使用此类批注检测缓冲区溢出。 有关添加批注的信息，请参阅[使用 SAL 注释减少 C /C++代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)并**批注函数参数和返回值**。

目前，仅非常量字符串缓冲区诊断并发出以下警告。 理想情况下，应批注作为函数参数传递或由函数返回的所有缓冲区。 数组**wchar\_t**或**char**适合使用此警告。 当前不是无符号的字符。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码示例将生成此警告。

```
int foo( LPTSTR buffer, size_t cch );  
```

下面的代码示例可避免此警告。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 SAL 注释减少 C/C++ 代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)

**对函数参数和返回值进行批注**
 

 






