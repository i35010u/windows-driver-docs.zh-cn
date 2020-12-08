---
title: C28741
description: 警告 C28741 函数中的批注缓冲区。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28741
ms.openlocfilehash: 3a6946fe6c5544845a760d7b9944a620d507dbee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823395"
---
# <a name="c28741"></a>C28741


警告 C28741：函数中的批注缓冲区

此警告表明，作为函数参数传递或由函数返回的缓冲区应使用 Microsoft 源代码批注语言 (SAL) 进行批注。 静态分析工具可使用此类注释来检测缓冲区溢出。

目前，此警告只诊断了非常量的字符串缓冲区。 理想情况下，所有作为函数参数传递或由函数返回的缓冲区都应进行批注。 **Wchar \_ t** 或 **char** 的数组是此警告的候选项。 无符号字符当前不是。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码示例将生成此警告。

```
  int foo( LPTSTR buffer, size_t cch );
```

下面的代码示例通过使用 SAL 注释 **\_ Out \_ 写入 \_** 来指定被调用函数写入缓冲区并且缓冲区不能为 NULL，从而避免出现此警告。 批注指示缓冲区是 *cch* 元素。

```
    int foo(_Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





