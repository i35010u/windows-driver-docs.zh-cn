---
title: C28170
description: 警告 C28170 函数已声明位于分页段中，但未找到 PAGED_CODE 或 PAGED_CODE_LOCKED 既不。
ms.assetid: 9efffcc8-54b6-46f8-b037-53c66a8eace2
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28170
ms.openlocfilehash: 8831016dc62669b36096bbb4ed3093730a50100c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546945"
---
# <a name="c28170"></a>C28170


警告 C28170:该函数具有声明位于分页的段中，但既不 PAGED\_代码，也不分页\_代码\_找到已锁定

代码分析工具将报告此错误时**\#杂注分配\_文本**或**\#杂注代码\_seg**用于移动不函数包含分页\_代码或 PAGED\_代码\_已锁定到可分页的代码部分的宏。 在对应的行号到第一个大括号报告此错误 (**{**) 函数中。

代码分析工具会推断出的节名称开头页时，部分是可分页。 可分页的代码中的函数必须包含 PAGED\_代码或 PAGED\_代码\_开头的第一个大括号之间的函数已锁定宏 (**{** ) 和第一个条件语句。

这些宏允许代码分析工具和运行时检查程序以确定是否可能在提升的 IRQL 运行可分页的代码。 如果在提升的权限级别运行系统时，将发生页面故障，系统将崩溃。

如果分页段中的函数随后将被锁定到内存中，使用 PAGED\_代码\_锁定而不是 PAGED\_代码。 页面\_代码\_已锁定宏，驱动程序进行调用，而不会遇到 PREfast for Drivers 引发 IRQL 警告。

这种情况通常是很难发现测试时 (除非 PAGED\_代码宏用于导致驱动程序验证程序，以检查是否出现错误)，因为该代码必须实际出页的页面错误发生。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

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

 

 





