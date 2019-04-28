---
title: .asm（更改反汇编选项）
description: .Asm 命令控制的反汇编代码的显示方式。
ms.assetid: c963c4f2-3bfc-4551-9b7b-74473a63eb11
keywords:
- 更改反汇编选项 (.asm) 命令
- 调试时，更改反汇编选项 (.asm) 命令的程序集
- .asm （更改反汇编选项） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .asm (Change Disassembly Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35a76cb9f8294411d07ee652e693060901165313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337000"
---
# <a name="asm-change-disassembly-options"></a>.asm（更改反汇编选项）


**.Asm**命令控制的反汇编代码的显示方式。

```dbgcmd
    .asm 
    .asm[-] Options
```

## <a name="span-idddkmetachangedisassemblyoptionsdbgspanspan-idddkmetachangedisassemblyoptionsdbgspanparameters"></a><span id="ddk_meta_change_disassembly_options_dbg"></span><span id="DDK_META_CHANGE_DISASSEMBLY_OPTIONS_DBG"></span>参数


<span id="_______-______"></span> **-**   
使指定的选项被禁用。 如果使用没有负号，则将启用指定的选项。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是任意数量的以下选项：

<span id="ignore_output_width"></span><span id="IGNORE_OUTPUT_WIDTH"></span>**ignore\_output\_width**  
使调试器无法检查在反汇编显示的线条的宽度。

<span id="no_code_bytes"></span><span id="NO_CODE_BYTES"></span>**no\_code\_bytes**  
（仅 x86 和 x64 目标）取消显示原始字节。

<span id="source_line"></span><span id="SOURCE_LINE"></span>**source\_line**  
反汇编的源代码的行号的每一行的前缀。

<span id="verbose"></span><span id="VERBOSE"></span>**verbose**  
（仅限 Itanium 目标）导致捆绑包类型信息与标准拆装信息一起显示。

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

有关程序集的调试和相关命令，请参阅[在程序集模式下调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

使用 **.asm**本身显示选项的当前状态。

此命令会影响调试器命令窗口中的任何反汇编指令的显示。 在 WinDbg 中它也会更改反汇编窗口的内容。

 

 





