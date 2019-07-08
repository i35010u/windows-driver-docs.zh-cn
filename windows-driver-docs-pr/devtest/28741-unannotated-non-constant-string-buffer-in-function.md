---
title: C28741
description: 警告 C28741 未批注缓冲区，该函数。
ms.assetid: 85F071C2-C91B-43D6-8F59-F1D1F955ECC1
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28741
ms.openlocfilehash: c8d4c02623eebce83909f33fd51d2375132886b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374733"
---
# <a name="c28741"></a>C28741


警告 C28741:在函数中的一个未批注的缓冲区

此警告指示作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可以使用此类批注检测缓冲区溢出。

目前，仅非常量字符串缓冲区诊断并发出以下警告。 理想情况下，应批注作为函数参数传递或由函数返回的所有缓冲区。 数组**wchar\_t**或**char**适合使用此警告。 当前不是无符号的字符。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的示例代码将生成此警告。

```
  int foo( LPTSTR buffer, size_t cch );
```

下面的代码示例使用 SAL 批注，因此可避免此警告 **\_出\_写入\_** 指定所调用的函数将写入缓冲区和缓冲区不能为 NULL。 该批注指示缓冲区是否属于*cch*元素。

```
    int foo(_Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





