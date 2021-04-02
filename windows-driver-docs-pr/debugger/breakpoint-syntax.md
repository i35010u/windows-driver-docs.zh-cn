---
title: 断点语法
description: 本主题介绍断点语法
keywords: 调试器，方法上的断点，断点，命令的语法规则，b (断点标识符) ，文本 MASM 标识符，模板化函数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4784be5944552103326be85359d3fcfbe7d744fe
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113612"
---
# <a name="breakpoint-syntax"></a>断点语法


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


在通过调试器命令窗口或通过 WinDbg 图形界面创建 [断点](using-breakpoints.md)时，可以使用以下语法元素。

### <a name="span-idaddresses_in_breakpointsspanspan-idaddresses_in_breakpointsspanaddresses-in-breakpoints"></a><span id="addresses_in_breakpoints"></span><span id="ADDRESSES_IN_BREAKPOINTS"></span>断点中的地址

断点支持多种类型的地址语法，包括虚拟地址、函数偏移量和源行号。 例如，你可以使用以下任一命令来设置断点：

```dbgcmd
0:000> bp 0040108c
0:000> bp main+5c
0:000> bp `source.c:31`
```

有关此语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)、 [源行语法](source-line-syntax.md)和各个命令主题。

### <a name="span-idbreakpoints_on_methodsspanspan-idbreakpoints_on_methodsspanbreakpoints-on-methods"></a><span id="breakpoints_on_methods"></span><span id="BREAKPOINTS_ON_METHODS"></span>方法上的断点

如果要在 *MyClass* 类中的 *MyMethod* 方法上放置断点，可以使用两种不同的语法：

-   在 MASM 表达式语法中，可以通过双冒号或双下划线来指示方法。

    ```dbgcmd
    0:000> bp MyClass::MyMethod 
    0:000> bp MyClass__MyMethod 
    ```

-   在 c + + 表达式语法中，必须使用双冒号指示方法。

    ```dbgcmd
    0:000> bp @@( MyClass::MyMethod ) 
    ```

如果要使用更复杂的断点命令，应使用 MASM 表达式语法。 有关表达式语法的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

### <a name="breakpoints-using-complicated-masm-expressions"></a>使用复杂的 MASM 表达式的断点

若要在复杂函数上设置断点（包括包含空格的函数以及 c + + 公共类的成员），请将该表达式括在括号中。 例如，使用 **bp (？MyPublic)** 或 **bp (new) 运算符**。

更通用的方法是使用 @！chars "语法。 这是 MASM 计算器中的特殊转义，可用于为符号解析提供任意文本。 必须以 @！开头的三个符号 并以引号 ( ") 结束。 如果没有此语法，则不能在 MASM 计算器的符号名称中使用空格、尖括号 (&lt; 、 &gt;) 或其他特殊字符。 此语法专用于名称，而不是参数。 模板和重载是需要此引号表示法的符号的主要来源。 还可以通过使用 @  ！chars "语法，如以下代码示例所示。

```dbgcmd
0:000> bu @!"ExecutableName!std::pair<unsigned int,std::basic_string<unsigned short,std::char_traits<unsigned short>,std::allocator<unsigned short> > >::operator="
```

在此示例中， *ExecutableName* 是可执行文件的名称。

此转义语法更适用于 c + + (例如，重载运算符) 而不是 C，因为 C 函数名称中不) 空格 (或特殊字符。 不过，对于许多托管代码而言，此语法也很重要，因为在 .NET Framework 中使用了重载。

若要在 c + + 语法中使用任意文本设置断点，请使用 <strong>bu @ @c + + (</strong><em>文本</em>**)** 用于 c + + 兼容的符号。

### <a name="breakpoints-in-scripts"></a>脚本中的断点

无需显式引用断点 Id。 相反，您可以使用解析为对应于断点 ID 的整数的数值表达式。 若要指示表达式应解释为断点，请使用以下语法。

```dbgcmd
b?[Expression]
```

在此语法中，方括号是必需的，并且 *表达式* 表示解析为对应于断点 ID 的整数的任何数值表达式。

此语法允许调试器脚本以编程方式选择断点。 在下面的示例中，断点会根据用户定义的伪寄存器的值发生变化。

```dbgcmd
b?[@$t0]
```

### <a name="breakpoint-pseudo-registers"></a>>断点 Pseudo-Registers

如果要在表达式中引用断点地址，可以将 [伪寄存器](pseudo-register-syntax.md) 与 **$bp**_Number_ 语法结合使用，其中 *number* 是断点 ID。 有关此语法的详细信息，请参阅 Pseudo-Register 语法。

 

 





