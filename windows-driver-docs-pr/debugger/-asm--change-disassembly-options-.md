---
title: .asm（更改反汇编选项）
description: .Asm 命令控制反汇编代码的显示方式。
keywords:
- " ( .asm) 命令更改反汇编选项"
- 程序集调试，更改反汇编选项 ( .asm) 命令
- .asm (更改反汇编选项) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .asm (Change Disassembly Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b3fc39442580d50935491ed6f606ac1349ba08c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800013"
---
# <a name="asm-change-disassembly-options"></a>.asm（更改反汇编选项）


**.Asm** 命令控制反汇编代码的显示方式。

```dbgcmd
    .asm 
    .asm[-] Options
```

## <a name="span-idddk_meta_change_disassembly_options_dbgspanspan-idddk_meta_change_disassembly_options_dbgspanparameters"></a><span id="ddk_meta_change_disassembly_options_dbg"></span><span id="DDK_META_CHANGE_DISASSEMBLY_OPTIONS_DBG"></span>参数


<span id="_______-______"></span> **-**   
使指定的选项被禁用。 如果不使用负号，将启用指定的选项。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列任意数量的选项：

<span id="ignore_output_width"></span><span id="IGNORE_OUTPUT_WIDTH"></span>**忽略 \_ 输出 \_ 宽度**  
阻止调试器检查反汇编显示中的行的宽度。

<span id="no_code_bytes"></span><span id="NO_CODE_BYTES"></span>**无 \_ 代码 \_ 字节**  
 (x86 和 x64 目标仅) 禁止显示原始字节。

<span id="source_line"></span><span id="SOURCE_LINE"></span>**源 \_ 行**  
用源代码的行号为每行反汇编加前缀。

<span id="verbose"></span><span id="VERBOSE"></span>**详细**  
 (仅限 Itanium 目标) 会导致随标准反汇编信息一起显示捆绑类型信息。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的说明，请参阅 [程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

使用 **.asm** 本身显示选项的当前状态。

此命令会影响调试器中的任何反汇编说明命令窗口。 在 WinDbg 中，它还更改了 "反汇编" 窗口的内容。

 

 





