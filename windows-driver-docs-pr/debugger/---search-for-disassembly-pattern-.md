---
title: '\# （搜索反汇编模式）'
description: 数字符号 （#） 命令会在反汇编代码中的指定模式搜索。
ms.assetid: 834dd432-94b8-4bf6-9318-09a118eab5ab
keywords:
- （搜索反汇编模式）Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Search for Disassembly Pattern)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25968c3ee037e332a0d532a6da9988b96261cc57
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566438"
---
# <a name="-search-for-disassembly-pattern"></a>\# （搜索反汇编模式）


数字符号 (**\#**) 命令搜索指定模式中的反汇编代码。

```dbgcmd
     # [Pattern] [Address [ L Size ]] 
```

## <a name="span-idddkcmdsearchfordisassemblypatterndbgspanspan-idddkcmdsearchfordisassemblypatterndbgspanparameters"></a><span id="ddk_cmd_search_for_disassembly_pattern_dbg"></span><span id="DDK_CMD_SEARCH_FOR_DISASSEMBLY_PATTERN_DBG"></span>参数


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定要搜索的反汇编代码中的模式。 *模式*可以包含各种通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。 如果你想要中包括空格*模式*，必须将模式括在引号中。 模式不是区分大小写的。 如果您曾经**\#** 命令，可省略*模式*，命令重用最近使用模式。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定搜索开始位置的地址。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
指定要搜索指令的数。 如果省略*大小*，搜索继续，直到出现第一个匹配项。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

调试和相关命令，请参阅有关程序集的详细信息[在程序集模式下调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果以前使用过**\#** 命令，可省略*地址*上, 一次搜索结束的地方开始执行搜索。

此命令通过搜索指定模式的已拆分的文本有效。 可以使用此命令在反汇编输出中查找注册名称、 常量或出现的任何其他字符串。 您可以重复该命令而无需*地址*参数查找模式的后续匹配项。

可以通过查看反汇编说明[ **u （反汇编）** ](u--unassemble-.md)命令或使用[反汇编窗口](disassembly-window.md)在 WinDbg 中。 反汇编显示包含最多四个部分：地址偏移量、 二进制代码、 汇编语言助记键和程序集语言的详细信息。 下面的示例显示了可能的显示。

```console
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

**\#** 命令可搜索的任何单个部分内的反汇编显示的文本。 例如，可以使用 **\# eax 0040116b**若要查找**mov eax\[ebp 0x1c\]** 地址 0040116 d 处的指令。 以下命令还可以找到此指令。

```console
#  [ebp?0x  0040116b 
#  mov  0040116b 
#  8945*  0040116b 
#  116d  0040116b 
```

但是，你不能搜索**mov eax\\*** 作为单个单元，因为**mov**并**eax**出现在显示的不同部分。 请改用**mov\*eax**。

又如，则可以发出以下命令以搜索到的第一个引用**strlen**函数的入口点之后**主要**。

```console
# strlen main
```

同样，您可以发出以下两个命令，以找到第一个**jnz**之后指令寻址 0x779F9FBA，然后找到下一步**jnz**之后的指令。

```console
# jnz 779f9fba# 
```

如果省略*模式*或*地址*，其值基于是因为先前使用**\#** 命令。 如果您省略两个参数中第一次发出**\#** 命令时，不执行任何搜索。 但是，值*模式*并*地址*即使在这种情况下初始化。

如果包括*模式*或*地址*，其值设置为输入的值。 如果省略*地址*，它将初始化为程序计数器的当前值。 如果省略*模式*，它将初始化为空的模式。

 

 





