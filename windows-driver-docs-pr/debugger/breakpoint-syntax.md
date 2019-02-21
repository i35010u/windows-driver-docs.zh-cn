---
title: 断点语法
description: 本主题介绍断点语法
ms.assetid: 86228b87-9ca3-4d0c-be9e-63446ac6ce31
keywords: 调试器，断点在方法、 断点、 命令、 b （断点标识符）、 文字 MASM 标识符和模板化函数的语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b714acd984506f36205285f0c61cd90e43c839b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542618"
---
# <a name="breakpoint-syntax"></a>断点语法


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


创建时，可使用以下语法元素[断点](using-breakpoints.md)，通过调试器命令窗口或 WinDbg 图形界面。

### <a name="span-idaddressesinbreakpointsspanspan-idaddressesinbreakpointsspanaddresses-in-breakpoints"></a><span id="addresses_in_breakpoints"></span><span id="ADDRESSES_IN_BREAKPOINTS"></span>中的断点的地址

断点支持许多类型的地址语法，包括虚拟地址、 函数偏移量和源行号。 例如，您可以使用任一以下命令以设置断点：

```dbgcmd
0:000> bp 0040108c
0:000> bp main+5c
0:000> bp `source.c:31`
```

有关此语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)，[源行语法](source-line-syntax.md)，以及单个命令的主题。

### <a name="span-idbreakpointsonmethodsspanspan-idbreakpointsonmethodsspanbreakpoints-on-methods"></a><span id="breakpoints_on_methods"></span><span id="BREAKPOINTS_ON_METHODS"></span>在方法上的断点

如果你想要放置一个断点*MyMethod*中的方法*MyClass*类，可以使用两个不同的语法：

-   在 MASM 表达式语法中，可以通过使用两个冒号或双下划线指示一种方法。

    ```dbgcmd
    0:000> bp MyClass::MyMethod 
    0:000> bp MyClass__MyMethod 
    ```

-   在 c + + 表达式语法中，必须通过使用两个冒号指示一种方法。

    ```dbgcmd
    0:000> bp @@( MyClass::MyMethod ) 
    ```

如果你想要使用更复杂的断点命令，应使用 MASM 表达式语法。 有关表达式语法的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

### <a name="span-idbreakpointsusingcomplicatedtextspanspan-idbreakpointsusingcomplicatedtextspanbreakpoints-using-complicated-text"></a><span id="breakpoints_using_complicated_text"></span><span id="BREAKPOINTS_USING_COMPLICATED_TEXT"></span>使用复杂的文本的断点

若要在复杂处设置断点函数，包括包含空格，以及 c + + 公共类的成员的函数将表达式括在括号中。 例如，使用**最佳实践 （??MyPublic)** 或**最佳实践 （new 运算符）**。

更灵活方法是使用 @ ！"字符"语法。 这是使你可以提供的符号解析的任意文本 MASM 计算器中是一种特殊转义。 必须以开头的三个符号 @ ！" 引号 （"） 开头和结尾。 而无需此语法中，您不能使用空格，尖括号 (&lt;， &gt;)，或在 MASM 计算器中的符号名称中的其他特殊字符。 此语法是以独占方式的名称，并不是参数。 模板和重载都需要此引号表示法的符号的主要来源。 您还可以设置**bu**命令通过使用 @ ！"字符"语法，如以下代码示例所示。

```dbgcmd
0:000> bu @!"ExecutableName!std::pair<unsigned int,std::basic_string<unsigned short,std::char_traits<unsigned short>,std::allocator<unsigned short> > >::operator="
```

在此示例中， *ExecutableName*是可执行文件的名称。

此转义语法是更适用于 c + + （例如，重载运算符） 而不是 C，因为没有空格 （或特殊字符） 中有 C 函数名称。 但是，此语法也很重要的托管代码大量由于大量使用.NET Framework 中的重载。

若要在 c + + 语法中的任意文本上设置断点，请使用<strong>bu @@c+ + (</strong><em>文本</em>**)** c + + 兼容符号。

### <a name="span-idbreakpointsinscriptsspanspan-idbreakpointsinscriptsspanbreakpoints-in-scripts"></a><span id="breakpoints_in_scripts"></span><span id="BREAKPOINTS_IN_SCRIPTS"></span>在脚本中的断点

断点 Id 不需要显式引用。 相反，可以使用数值表达式解析为一个整数，对应于断点 id。 若要指示应将表达式解释为一个断点，请使用以下语法。

```dbgcmd
b?[Expression]
```

在此语法中，方括号是必需的并且*表达式*代表的任何数值表达式，将解析为一个整数，对应于断点 id。

此语法允许调试器脚本以编程方式选择一个断点。 在以下示例中，具体取决于用户定义的伪寄存器的值发生更改断点。

```dbgcmd
b?[@$t0]
```

### <a name="span-idbreakpointpseudoregistersspanspan-idbreakpointpseudoregistersspanbreakpoint-pseudo-registers"></a><span id="breakpoint_pseudo_registers"></span><span id="BREAKPOINT_PSEUDO_REGISTERS"></span>断点伪寄存器

如果你想要在表达式中的断点地址是指，则可以使用[伪寄存器](pseudo-register-syntax.md)使用 **$bp * * * 数*语法，其中*数*是断点 id。 有关此语法的详细信息，请参阅伪寄存器语法。

 

 





