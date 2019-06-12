---
title: WinDbg 和其他 Windows 调试器中的条件断点
description: 需要满足特定条件时，才中断时，WinDbg 和其他 Windows 调试器中的条件断点很有用。
ms.assetid: 9fa5b417-8904-48bc-ad5c-62ba35d70b73
keywords:
- 断点条件
- 条件断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5687bf16b7330076ec81802772c02f9110f16a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381985"
---
# <a name="conditional-breakpoints-in-windbg-and-other-windows-debuggers"></a>WinDbg 和其他 Windows 调试器中的条件断点


需要满足特定条件时，才中断时，WinDbg 和其他 Windows 调试器中的条件断点很有用。

## <span id="ddk_setting_a_conditional_breakpoint_dbg"></span><span id="DDK_SETTING_A_CONDITIONAL_BREAKPOINT_DBG"></span>


通过组合使用断点命令来创建条件断点[ **j （执行如果-其他）** ](j--execute-if---else-.md)命令或[**如果**](-if.md)令牌后, 跟[ **gc （从条件性断点转）** ](gc--go-from-conditional-breakpoint-.md)命令。 此断点会引起的中断来满足特定条件时才会出现。

条件断点使用的基本语法**j**命令如下所示：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' "
```

条件断点使用的基本语法 **.if**令牌如下所示：

```dbgcmd
0:000> bp Address ".if (Condition) {OptionalCommands} .else {gc}"
```

因此最好通过一个示例进行说明条件断点。 下面的命令行 143 Mysource.cpp 源文件的处设置断点。 命中此断点时，变量**MyVar**进行测试。 如果此变量是小于或等于 20，执行将继续;如果超过 20，执行将停止。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' " 
0:000> bp `mysource.cpp:143` ".if (poi(MyVar)>0n20) {} .else {gc}"
```

上述命令包含一种相当复杂的语法，其中包含以下元素：

-   [**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令设置断点。 虽然前面的示例中使用的最佳实践命令，但您还可以使用**bu （设置无法解析断点）** 命令。 有关详细信息之间的差异**bp**和**bu**，和断点的基本简介，请参阅[使用断点](using-breakpoints.md)。

-   通过使用抑音符指定源行号 ( **\`** )。 有关详细信息，请参阅[源行语法](source-line-syntax.md)。

-   当命中断点、 直引号中的命令 ( **"** ) 执行。 在此示例中，此命令是[ **j （执行如果-其他）** ](j--execute-if---else-.md)命令或[**如果**](-if.md)令牌，在括号中测试表达式。

-   在源应用程序， **MyVar**是一个整数。 如果使用的C++表达式语法**MyVar**解释为整数。 但是，在此示例中 （和默认调试程序配置中），使用 MASM 表达式语法。 在 MASM 表达式中， **MyVar**视为一个地址。 因此，您需要使用**poi**要对其取消引用运算符。 (如果您的变量实际上是 C 指针，您将需要取消引用指针它两次--例如， **poi(poi(MyPtr))** 。)**0n**前缀指定此数字是小数。 有关语法的详细信息，请参阅[MASM 数字和运算符](masm-numbers-and-operators.md)。

-   中括号的表达式后跟用单引号括起来的两个命令 ( **'** ) 用于**j**命令和大括号 ( {} ) 为 **。 如果**令牌。 如果表达式为 true，则执行这些命令的第一个。 在此示例中，没有第一个命令，因此命令执行将结束并使用调试器控件仍将保留。 如果在括号中的表达式为 false，将执行第二个命令。 第二个命令几乎始终应[ **gc （从条件性断点转）** ](gc--go-from-conditional-breakpoint-.md)命令，因为此命令会导致执行相同的方式在该断点之前出现的恢复已命中 （单步执行跟踪，或无执行）。

如果你想要每次时看到一条消息传递断点或它最后命中时，可以使用单引号引起来或用大括号中的其他命令。 例如：

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
0:000> bp `:143` ".if (poi(MyVar)>5) {.echo MyVar Too Big} .else {.echo MyVar Acceptable; gc} " 
```

这些注释是特别有用，如果你有多个运行在同一时间，此类断点，因为调试器不会显示其标准"断点*n*命中"消息时使用的命令字符串中**bp**命令。

### <a name="span-idconditionalbreakpointbasedonstringcomparisonspanspan-idconditionalbreakpointbasedonstringcomparisonspanspan-idconditionalbreakpointbasedonstringcomparisonspanconditional-breakpoint-based-on-string-comparison"></a><span id="Conditional_Breakpoint_Based_on_String_Comparison"></span><span id="conditional_breakpoint_based_on_string_comparison"></span><span id="CONDITIONAL_BREAKPOINT_BASED_ON_STRING_COMPARISON"></span>基于字符串比较的条件断点

在某些情况下你可能想要中断调试器，仅当与模式匹配的字符串变量。 例如，假设你想要中断 kernel32 ！仅当 CreateEventW *lpName*自变量指向的字符串与模式匹配"Global\*"。 下面的示例演示如何创建条件断点。

```dbgcmd
bp kernel32!CreateEventW "$$<c:\\commands.txt"
```

在前面[ **bp** ](bp--bu--bm--set-breakpoint-.md)命令将创建根据条件和一个名为 commands.txt 的脚本文件中的可选命令断点。 脚本文件包含以下语句。

```dbgcmd
.if (@r9 != 0) { as /mu ${/v:EventName} @r9 } .else { ad /q ${/v:EventName} }
.if ($spat(@"${EventName}", "Global*") == 0)  { gc } .else { .echo EventName }
```

*LpName*自变量传递给**CreateEventW**函数是第四个参数，因此它存储在 r9 寄存器 (x 处理器）。 此脚本执行以下步骤：

1.  如果*lpName*是不为 NULL，请使用[**作为**](as--as--set-alias-.md)并[ **${}**  ](-------alias-interpreter-.md)若要创建一个别名事件名称。 将以 null 结尾 Unicode 字符串开始的指向的地址分配给 EventName *lpName*。 但是，如果*lpName*为 NULL，使用[ **ad** ](ad--delete-alias-.md)删除任何现有别名命名事件名称。

2.  使用[ **$spat** ](masm-numbers-and-operators.md)若要比较的字符串表示事件名称模式为"Global\*"。 如果字符串与模式不匹配，则使用[ **gc** ](gc--go-from-conditional-breakpoint-.md)继续但不会中断。 如果字符串与模式匹配，则拆分并显示由事件名称的字符串。

**请注意**  [ **$spat** ](masm-numbers-and-operators.md)执行不区分大小写的匹配项。

**请注意**  & 符 （@） 美元 spat(@"${EventName}"specifies that the string represented by EventName is to be interpreted literally; that is, a backslash ( \\ ) 中的字符将被视为一个反斜杠而不是一种转义字符。

### <a name="span-idconditionalbreakpointsandregistersignextensionspanspan-idconditionalbreakpointsandregistersignextensionspanconditional-breakpoints-and-register-sign-extension"></a><span id="conditional_breakpoints_and_register_sign_extension"></span><span id="CONDITIONAL_BREAKPOINTS_AND_REGISTER_SIGN_EXTENSION"></span>条件断点和寄存器符号扩展

可以设置断点是有条件的寄存器值。

以下命令将中断的开始处**myFunction**函数如果**eax**注册等于 0xA3:

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xa3  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xa3  {} .else {gc}"
```

但是，以下类似的命令将不一定会中断时**eax**等于 0xC0004321:

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xc0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xc0004321  {} .else {gc}"
```

上述命令将失败的原因是，MASM 表达式计算器补符号位的高等于一寄存器。 当**eax**具有值 0xC0004321，将被视为 0xFFFFFFFF\`C0004321 中计算-即使**eax**仍将显示为 0xC0004321。 但是，数字**0xc0004321**是带符号扩展在内核模式下，但不是在用户模式下。 因此前, 一个命令将无法正常工作在用户模式下。 如果掩码的高位**eax**，该命令将在内核模式下-正常工作，但现在它将在用户模式下失败。

您应该制定你的命令应进行防备针对这两种模式中的符号扩展。 在上述命令中，您可以使该命令防御性的高 32 位寄存器的位屏蔽使用 AND 运算来组合和 0x00000000\`FFFFFFFF 和通过包括的重读符号 (屏蔽高位的数值常量 **\`**  ) 其语法中。

以下命令将在用户模式和内核模式下正常工作：

```dbgcmd
0:000> bp mydriver!myFunction "j (@eax & 0x0`ffffffff) = 0x0`c0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if (@eax & 0x0`ffffffff) = 0x0`c0004321  {} .else {gc}"
```

有关哪些数字是由调试器符号扩展的详细信息，请参阅[符号扩展](sign-extension.md)。

### <a name="span-idconditionalbreakpointsinwindbgspanspan-idconditionalbreakpointsinwindbgspanconditional-breakpoints-in-windbg"></a><span id="conditional_breakpoints_in_windbg"></span><span id="CONDITIONAL_BREAKPOINTS_IN_WINDBG"></span>在 WinDbg 中的条件断点

在 WinDbg 中，可以创建条件断点通过单击[断点](edit---breakpoints.md)从**编辑**菜单中，输入一个新断点地址**命令**框中，并输入为条件**条件**框。

例如，如果键入**mymod ！ myFunc + 0x3A**成**命令**框和**myVar &lt; 7**到**条件**框等效于发出以下命令：

```dbgcmd
0:000> bu mymod!myFunc+0x3A "j(myVar<7) '.echo "Breakpoint hit, condition myVar<7"'; 'gc'" 
0:000> bu mymod!myFunc+0x3A ".if(myVar<7) {.echo "Breakpoint hit, condition myVar<7"} .else {gc}" 
```

### <a name="span-idrestrictionsonconditionalbreakpointsspanspan-idrestrictionsonconditionalbreakpointsspanrestrictions-on-conditional-breakpoints"></a><span id="restrictions_on_conditional_breakpoints"></span><span id="RESTRICTIONS_ON_CONDITIONAL_BREAKPOINTS"></span>条件断点的限制

你是否[控制用户模式下的调试程序与内核调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，不能使用条件断点或任何其他断点命令字符串包含[ **gc （转到从条件断点）** ](gc--go-from-conditional-breakpoint-.md)或[ **g （转向）** ](g--go-.md)命令。 如果使用这些命令，串行接口可能无法及时了解若干断点传递，并将不能返回到 CDB 中断。

 

 





