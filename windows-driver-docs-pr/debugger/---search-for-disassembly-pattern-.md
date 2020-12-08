---
title: '\# (搜索反汇编模式) '
description: '数字符号 ( # ) 命令在反汇编代码中搜索指定的模式。'
keywords:
- " (搜索反汇编模式) Windows 调试"
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Search for Disassembly Pattern)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f139e61d04b342c32544afd940b06f88c7a76218
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800193"
---
# <a name="-search-for-disassembly-pattern"></a>\# (搜索反汇编模式) 


数字符号 (**\#**) 命令在反汇编代码中搜索指定的模式。

```dbgcmd
     # [Pattern] [Address [ L Size ]] 
```

## <a name="span-idddk_cmd_search_for_disassembly_pattern_dbgspanspan-idddk_cmd_search_for_disassembly_pattern_dbgspanparameters"></a><span id="ddk_cmd_search_for_disassembly_pattern_dbg"></span><span id="DDK_CMD_SEARCH_FOR_DISASSEMBLY_PATTERN_DBG"></span>参数


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定要在反汇编代码中搜索的模式。 *模式* 可以包含各种通配符和说明符。 有关语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。 如果要在 *模式* 中包含空格，则必须用引号将模式引起来。 此模式不区分大小写。 如果以前使用过该 **\#** 命令并且省略了 *模式*，则该命令将重用最近使用的模式。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定搜索开始处的地址。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
指定要搜索的指令数。 如果省略 *大小*，搜索将继续，直到发生第一个匹配项。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的详细信息，请参阅 [程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果你以前使用过该 **\#** 命令并且省略了 *Address*，搜索将从上一个搜索结束的位置开始。

此命令通过搜索指定模式的反汇编文本来运行。 您可以使用此命令查找寄存器名称、常量或在反汇编输出中出现的任何其他字符串。 可以不带 *Address* 参数重复此命令，以便查找该模式的后续匹配项。

您可以使用 [**u (Unassemble)**](u--unassemble-.md) 命令或使用 WinDbg 的 " [反汇编" 窗口](disassembly-window.md) 查看反汇编说明。 反汇编显示最多包含四个部分：地址偏移量、二进制代码、程序集语言助记键和程序集语言详细信息。 下面的示例演示了可能的显示。

```console
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

**\#** 命令可以在反汇编显示的任何单个部分内搜索文本。 例如，可以使用 **\# eax 0040116b** 在 address 0040116d 上查找 **mov eax \[ 0x1c \]** 指令。 以下命令也会找到此指令。

```console
#  [ebp?0x  0040116b 
#  mov  0040116b 
#  8945*  0040116b 
#  116d  0040116b 
```

但是，您不能将 **mov eax \\** _ 作为单个单元来搜索，因为 _ *mov** 和 **eax** 显示在显示的不同部分。 请改用 " **mov \* eax**"。

作为另一个示例，你可以发出以下命令，搜索 **入口点后** 首次对 **strlen** 函数的引用。

```console
# strlen main
```

同样，你可以发出以下两个命令来查找地址0x779F9FBA 之后的第一个 **jnz** 指令，并在之后查找下一个 **jnz** 说明。

```console
# jnz 779f9fba# 
```

省略 *模式* 或 *地址* 时，它们的值基于以前使用的 **\#** 命令。 如果首次发出命令时省略任一参数 **\#** ，则不会执行任何搜索。 但是，即使在这种情况下，也会初始化 *Pattern* 和 *Address* 的值。

如果包括 *模式* 或 *地址*，则将其值设置为输入的值。 如果省略 *Address*，则会将其初始化为程序计数器的当前值。 如果省略 *模式*，则将其初始化为空模式。

 

 





