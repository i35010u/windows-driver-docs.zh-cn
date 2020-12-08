---
title: C28615
description: '警告 C28615 必须在 __try 块中调用 _alloca 时，__except ( # A1 块调用 _resetstkoflw。 不要从 catch ( # A1 块内调用 _resetstkoflw。'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28615
ms.openlocfilehash: 36e3a41f2ec06c13bfc3d3f14e9f3dbd0ead279e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823399"
---
# <a name="c28615"></a>C28615


警告 C28615：在 \_ \_ \_ \_ try 块中调用 alloca 时，必须在 except ( # A1 块 \_ 中调用 resetstkoflw \_ 。 不要 \_ 从 catch ( # A1 块中调用 resetstkoflw

当应用程序调用 catch 块中的 **\_ resetstkoflw** 函数时，或者当应用程序在 try 块中调用 **alloca** ，而不在 except 块中调用 **\_ resetstkoflw** 时，代码分析工具将报告此警告。

仅当调用 **\_ alloca**) 时，线程才能捕获一个堆栈溢出异常 (引发，除非堆栈被修复 (例如，在每个异常之后 **\_ resetstkoflw**) 。 如果从 **\_ alloca** 引发第一个异常后不修复堆栈，则第二个异常将导致立即终止进程终止。

当当前堆栈指针指向的地址比堆栈上的第三页大时，必须调用 **\_ resetstkoflw** 。 这是因为，在当前页面中，堆栈指针指向 (或将在一段时间内指向) ，这并无意义。

不应从结构化异常处理程序筛选器表达式或从结构化异常处理程序筛选表达式中调用的函数中调用 **\_ resetstkoflw** 函数。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

在以下示例中，代码分析工具将报告此警告，因为在堆栈展开之前会调用筛选器表达式。 如果堆栈溢出，则当当前堆栈指针指向堆栈底部的第三页时，将调用筛选器表达式。

```
__try 
{
    /* The following could cause stack overflow */
    char *x = _alloca (i);
}
__except ((GetExceptionCode () == EXCEPTION_STACK_OVERFLOW) 
    ? (_resetstkoflw (), EXCEPTION_EXECUTE_HANDLER) 
    : EXCEPTION_CONTINUE_SEARCH)
{
}
```

由于类似的原因，下面的示例也会失败。

```

__try 
{
 char *x = _alloca (i);
}
__except (SEHFilter (GetExceptionCode ()))
{
}

int SEHFilter (DWORD dwExceptionCode)
{
 if (dwExceptionCode == EXCEPTION_STACK_OVERFLOW)
 {
 _resetstkoflw ();
 return EXCEPTION_EXECUTE_HANDLER;
 }
 else
 {
 return EXCEPTION_CONTINUE_SEARCH;
 }
}
```

下面的示例成功避免了此错误。

```
__try
{
    char *x = _alloca (i);
}
__except ((GetExceptionCode () == EXCEPTION_STACK_OVERFLOW) ? EXCEPTION_EXECUTE_HANDLER : EXCEPTION_CONTINUE_SEARCH)
{
    // In this block the stack has already been unwound,
    // so this call will succeed.
_resetstkoflw ();
}
```









