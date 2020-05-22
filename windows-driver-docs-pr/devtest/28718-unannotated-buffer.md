---
title: C28718
description: 警告 C28718 批注缓冲区。
ms.assetid: 8417AB73-B645-451D-A359-9A66A793A78D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28718
ms.openlocfilehash: e070adf110ed1a1a5f12c55565f7c9f77b10ebbf
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769723"
---
# <a name="c28718"></a>C28718


警告 C28718：批注缓冲区

当传递到函数或由函数返回的缓冲区没有源代码注释语言（SAL）批注时，将报告此警告。 静态分析工具可使用此类注释来检测缓冲区溢出。 有关添加注释的信息，请参阅[使用 SAL 注释减少 C/c + + 代码缺陷](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)。

目前，此警告只诊断了非常量的字符串缓冲区。 理想情况下，所有作为函数参数传递或由函数返回的缓冲区都应进行批注。 **Wchar \_ t**或**char**的数组是此警告的候选项。 无符号字符当前不是。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码示例将生成此警告。

```
int foo( LPTSTR buffer, size_t cch );  
```

下面的代码示例可避免此警告。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 SAL 注释减少 C/C++ 代码缺陷](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)


 

 






