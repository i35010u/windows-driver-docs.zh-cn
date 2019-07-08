---
title: C28615
description: 警告 C28615 必须在 __except 块中调用 _resetstkoflw，__try 块中调用 _alloca 时。 不要调用 _resetstkoflw 从 catch （） 块内。
ms.assetid: bccfc846-58b9-4c20-bbe7-383ecf836165
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28615
ms.openlocfilehash: e16ac49d93310cd045eda6d9acd43c977c06e76f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384128"
---
# <a name="c28615"></a>C28615


警告 C28615:必须调用\_中的 resetstkoflw \_ \_except() 块时调用\_中的 alloca \_ \_try 块。 不要调用\_resetstkoflw 从 catch （） 块内

代码分析工具将报告此警告，如果应用程序调用 **\_resetstkoflw** catch 块中，或者当应用程序调用的函数**alloca**中而无需调用的 try 块 **\_resetstkoflw**中 except 块。

线程可以捕获只有一个堆栈溢出异常 (通过调用引发 **\_alloca**) 除非修复堆栈 (例如，通过 **\_resetstkoflw**) 后每个异常. 如果堆栈不固定后的第一个异常引发从 **\_alloca**，第二个异常会导致立即和无提示的进程终止。

必须调用 **\_resetstkoflw**时当前堆栈指针指向高于在堆栈上的第三页的地址。 这是因为它没有任何意义，以使超出当前堆栈指针所指向的页保护页 （或在稍后将指向）。

**\_Resetstkoflw**从结构化的异常处理程序筛选器表达式，或从结构化的异常处理程序筛选器表达式调用的函数，不应调用函数。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

因为筛选表达式调用堆栈展开之前，代码分析工具将报告此警告对于下面的示例。 当有堆栈溢出时，当前堆栈指针所指向的第三页从堆栈的底部时调用的筛选器表达式。

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

下面的示例出于类似原因无法正常工作。

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

下面的示例成功可避免此错误。

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









