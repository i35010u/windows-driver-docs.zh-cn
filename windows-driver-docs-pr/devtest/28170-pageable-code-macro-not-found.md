---
title: C28170
description: 警告 C28170 已将函数声明为位于分页段中，但未找到 PAGED_CODE 和 PAGED_CODE_LOCKED。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28170
ms.openlocfilehash: 937ec7aa1b125d51eb0f5bd470b3d19c45b091d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838155"
---
# <a name="c28170"></a>C28170


警告 C28170：该函数已被声明为位于分页段中，但找不到分页 \_ 代码和 \_ \_ 锁定的分页代码

当 **\# 杂注分配 \_ 文本** 或 **\# 杂注代码 \_ seg** 用于将不包含分页代码的函数 \_ 或被分页代码 \_ 锁定的宏移到可 \_ 分页代码部分时，代码分析工具将报告此错误。 此错误是在函数中与第一个大括号 (**{**) 对应的行号处报告的。

当节名称以 PAGE 开头时，代码分析工具将推断节是可分页的。 可分页代码中的函数必须在 \_ \_ \_ 第一个大括号 (**{** ) 和第一个条件语句之间的函数开头包含分页的代码或分页代码锁定的宏。

这些宏允许代码分析工具和运行时检查器确定可分页代码是否可以在提升的 IRQL 上运行。 如果在系统以提升的级别运行时出现页错误，系统会崩溃。

如果分页段中的函数随后被锁定到内存中，则使用 \_ \_ 锁定的分页代码而不是分页 \_ 代码。 页 \_ 代码 \_ 锁定宏允许驱动程序发出引发 IRQL 的调用，而不会遇到驱动程序的 PREfast 警告。

此情况通常很难在测试 (的情况下找到，除非 \_ 使用分页代码宏来导致驱动程序验证程序检查) 错误，因为代码必须实际被分页出来才能出现页错误。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
void func();
#pragma alloc_text("PAGED_CODE", func);

void func1()
{
   // paged, no PAGED_CODE: error
}
```

下面的代码示例可避免此警告。

```
void func();
#pragma alloc_text("PAGED_CODE", func);

void func2()
{
   PAGED_CODE(); // includes PAGED_CODE macro
}
```

 

 





