---
title: WinDbg 和其他 Windows 调试器中的条件断点
description: 如果仅在满足特定条件时才需要中断，则 WinDbg 和其他 Windows 调试器中的条件断点很有用。
keywords:
- 断点，条件
- 条件断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42320b4c5ab03ab6abdfb655d22119a7ebc80d82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840431"
---
# <a name="conditional-breakpoints-in-windbg-and-other-windows-debuggers"></a>WinDbg 和其他 Windows 调试器中的条件断点


如果仅在满足特定条件时才需要中断，则 WinDbg 和其他 Windows 调试器中的条件断点很有用。

## <span id="ddk_setting_a_conditional_breakpoint_dbg"></span><span id="DDK_SETTING_A_CONDITIONAL_BREAKPOINT_DBG"></span>


条件断点是通过以下方式创建的：将断点命令与 [**j (Execute If-Else)**](j--execute-if---else-.md) 命令或 [**. If**](-if.md) 标记，后跟 [**gc (从条件断点)**](gc--go-from-conditional-breakpoint-.md) 命令进行组合。 此断点仅在满足特定条件时才会产生中断。

使用 **j** 命令的条件断点的基本语法如下所示：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' "
```

使用的条件断点的基本语法 **。如果** 令牌如下所示：

```dbgcmd
0:000> bp Address ".if (Condition) {OptionalCommands} .else {gc}"
```

使用示例可以最恰当地说明条件断点。 以下命令在 Mysource 源文件的第143行设置一个断点。 命中此断点时，将测试变量 **MyVar** 。 如果此变量小于或等于20，则继续执行;如果超过20，将停止执行。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' " 
0:000> bp `mysource.cpp:143` ".if (poi(MyVar)>0n20) {} .else {gc}"
```

前面的命令具有一个相当复杂的语法，其中包含以下元素：

-   [**Bp (设置断点)**](bp--bu--bm--set-breakpoint-.md)命令设置断点。 尽管前面的示例使用了 bp 命令，但你也可以使用 **bu (设置未解析的断点)** 命令。 有关 **最佳实践** 和 **bu** 之间的差异的详细信息，请参阅 [使用断点](using-breakpoints.md)。

-   使用抑音符 ( ) 指定源行号 **\`** 。 有关详细信息，请参阅 [源行语法](source-line-syntax.md)。

-   命中断点时，将执行 ( **"** ) 的直引号命令。 在此示例中，此命令是一个 [**j (如果为-Else)**](j--execute-if---else-.md) 命令，则为; [**如果**](-if.md) 为，则会测试括号中的表达式。

-   在源程序中， **MyVar** 是一个整数。 如果使用 c + + 表达式语法， **MyVar** 将解释为一个整数。 但是，在此示例中 (和默认调试器配置) 中，使用 MASM 表达式语法。 在 MASM 表达式中， **MyVar** 被视为地址。 因此，您需要使用 **poi** 运算符来取消引用它。  (如果你的变量实际上是 C 指针，则需要将其取消引用两次--例如， **poi (poi (MyPtr) # B4**。 ) **0n** 前缀指定此数字为 decimal。 有关语法的详细信息，请参阅 [MASM 数字和运算符](masm-numbers-and-operators.md)。

-   括号中的表达式后跟两个命令，用单引号括起来， ( **"** ) 用于 **j** 命令，将大括号 ( {} ) 用于 **。 if** 标记。 如果表达式为 true，则执行其中的第一个命令。 在此示例中，没有第一个命令，因此命令执行将结束，并控制将保留在调试器中。 如果括号中的表达式为 false，则将执行第二个命令。 第二个命令几乎始终是一个 [**gc (从条件断点)**](gc--go-from-conditional-breakpoint-.md) 命令，因为此命令导致执行恢复的方式与断点之前发生的方式相同 (步进、跟踪或自由执行) 。

如果要在每次传递断点时查看消息，或在最后一次命中断点时查看消息，则可以使用单引号或大括号中的其他命令。 例如：

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
0:000> bp `:143` ".if (poi(MyVar)>5) {.echo MyVar Too Big} .else {.echo MyVar Acceptable; gc} " 
```

如果同时运行多个此类断点，则这些注释特别有用，因为当你使用 **bp** 命令中的命令字符串时，调试器不会显示其标准 "断点 *n* 命中" 消息。

### <a name="span-idconditional_breakpoint_based_on_string_comparisonspanspan-idconditional_breakpoint_based_on_string_comparisonspanspan-idconditional_breakpoint_based_on_string_comparisonspanconditional-breakpoint-based-on-string-comparison"></a><span id="Conditional_Breakpoint_Based_on_String_Comparison"></span><span id="conditional_breakpoint_based_on_string_comparison"></span><span id="CONDITIONAL_BREAKPOINT_BASED_ON_STRING_COMPARISON"></span>基于字符串比较的条件断点

在某些情况下，仅当字符串变量与模式匹配时，才需要中断调试器。 例如，假设要在 kernel32.dll 处中断！仅当 *lpName* 参数指向与模式 "Global" 匹配的字符串时，CreateEventW \* 。 下面的示例演示如何创建条件断点。

```dbgcmd
bp kernel32!CreateEventW "$$<c:\\commands.txt"
```

上述 [**bp**](bp--bu--bm--set-breakpoint-.md) 命令基于在名为 commands.txt 的脚本文件中的条件和可选命令创建断点。 脚本文件包含以下语句。

```dbgcmd
.if (@r9 != 0) { as /mu ${/v:EventName} @r9 } .else { ad /q ${/v:EventName} }
.if ($spat(@"${EventName}", "Global*") == 0)  { gc } .else { .echo EventName }
```

传递给 **CreateEventW** 函数的 *lpName* 参数是第四个参数，因此它存储在 r9 register)  (x64 处理器。 此脚本执行以下步骤：

1.  如果 *lpName* 不为 NULL，则使用 [**as**](as--as--set-alias-.md)和 [**$ {}**](-------alias-interpreter-.md)创建名为 "名称名称" 的别名。 分配以指定以 null 结尾的 Unicode 字符串，以 *lpName* 所指向的地址开头。 另一方面，如果 *lpName* 为 NULL，请使用 [**ad**](ad--delete-alias-.md) 删除任何名为 "名称名称" 的现有别名。

2.  使用 [**$spat**](masm-numbers-and-operators.md) 将由事件名称表示的字符串与模式 "Global" 进行比较 \* 。 如果字符串与模式不匹配，请使用 [**gc**](gc--go-from-conditional-breakpoint-.md) 继续而不中断。 如果字符串与模式匹配，则中断并显示由事件名称表示的字符串。

**请注意**  [**$spat**](masm-numbers-and-operators.md) 执行不区分大小写的匹配。

**注意**  $Spat ( @ "$ {名称}" 中 ( @ ) 字符的与号指定为按字面解释指定的字符串;也就是说，) 的反斜杠 ( \\ 被视为反斜杠而不是转义字符。

### <a name="span-idconditional_breakpoints_and_register_sign_extensionspanspan-idconditional_breakpoints_and_register_sign_extensionspanconditional-breakpoints-and-register-sign-extension"></a><span id="conditional_breakpoints_and_register_sign_extension"></span><span id="CONDITIONAL_BREAKPOINTS_AND_REGISTER_SIGN_EXTENSION"></span>条件断点和注册签名扩展

可以设置在寄存器值上有条件的断点。

如果 **eax** 寄存器等于0xA3，则以下命令将在 **myFunction** 函数的开头处中断：

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xa3  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xa3  {} .else {gc}"
```

但是，当 **eax** 等于0xC0004321 时，以下类似的命令不一定会中断：

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xc0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xc0004321  {} .else {gc}"
```

上述命令将失败的原因是，MASM 表达式计算器会将高位符号扩展为1。 当 **eax** 值为0xC0004321 时，它将 \` 在计算中被视为 0xffffffff C0004321，即使 **eax** 仍将显示为0xC0004321。 但是，在内核模式下，数字 **0xc0004321** 是带符号扩展的，而不是在用户模式下。 因此，在用户模式下，上述命令将无法正常运行。 如果你屏蔽了 **eax** 的高位，则该命令将在内核模式下正常工作-但现在它在用户模式下会失败。

你应该在这两种模式下，为保守的命令构建命令。 在前面的命令中，可以通过使用和操作将32位寄存器的高位与 0x00000000 \` FFFFFFFF 合并，并通过 **\`** 在其语法中包含一个 ( ) 来屏蔽数值常量的高位，从而使命令具有更强的防御性。

以下命令将在用户模式和内核模式下正常工作：

```dbgcmd
0:000> bp mydriver!myFunction "j (@eax & 0x0`ffffffff) = 0x0`c0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if (@eax & 0x0`ffffffff) = 0x0`c0004321  {} .else {gc}"
```

有关调试器由哪些数字进行符号扩展的详细信息，请参阅 [签名扩展](sign-extension.md)。

### <a name="span-idconditional_breakpoints_in_windbgspanspan-idconditional_breakpoints_in_windbgspanconditional-breakpoints-in-windbg"></a><span id="conditional_breakpoints_in_windbg"></span><span id="CONDITIONAL_BREAKPOINTS_IN_WINDBG"></span>WinDbg 中的条件断点

在 WinDbg 中，可以通过在 "**编辑**" 菜单中选择 "[断点](edit---breakpoints.md)"，在 "**命令**" 框中输入新的断点地址，然后在 "**条件**" 框中输入一个条件来创建条件断点。

例如，在 "**命令**" 框中键入 **mymod！ myFunc + 0x3A** ，在 "**条件**" 框中键入 **myVar &lt; 7** 等效于发出以下命令：

```dbgcmd
0:000> bu mymod!myFunc+0x3A "j(myVar<7) '.echo "Breakpoint hit, condition myVar<7"'; 'gc'" 
0:000> bu mymod!myFunc+0x3A ".if(myVar<7) {.echo "Breakpoint hit, condition myVar<7"} .else {gc}" 
```

### <a name="span-idrestrictions_on_conditional_breakpointsspanspan-idrestrictions_on_conditional_breakpointsspanrestrictions-on-conditional-breakpoints"></a><span id="restrictions_on_conditional_breakpoints"></span><span id="RESTRICTIONS_ON_CONDITIONAL_BREAKPOINTS"></span>条件断点的限制

如果要 [从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，则不能使用条件断点或包含 [**Gc (从条件断点)**](gc--go-from-conditional-breakpoint-.md) 或 [**g (中转)**](g--go-.md) 命令的任何其他断点命令字符串。 如果你使用这些命令，则串行接口可能无法跟上断点传递次数，并且你将无法返回到 CDB。

 

 





