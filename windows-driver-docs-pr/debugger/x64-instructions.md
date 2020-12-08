---
title: x64 指令
description: x64 指令
keywords:
- x64 处理器，说明
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2767ff96f42acfb3e4bd6cc61129ec3b93f65de8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802719"
---
# <a name="x64-instructions"></a>x64 指令


## <span id="ddk_x64_instructions_dbg"></span><span id="DDK_X64_INSTRUCTIONS_DBG"></span>


大多数 x86 指令在64位模式下仍适用于 x64。 在64位模式下不再支持某些很少使用的操作，例如：

-   二进制编码的十进制算术指令： AAA，AAD，AAM，.AAS，DAA，DAS

-   绑定

-   PUSHAD 和 POPAD

-   对段寄存器（如推送 DS 和 POP DS）进行处理的大多数操作。 使用 FS 或 GS 段寄存器 (操作仍然有效。 ) 

X64 指令集包括最新的 x86 添加到 x86，如 SSE 2。 针对 x64 编译的程序可以自由地使用这些说明。

### <a name="span-iddata_transferspanspan-iddata_transferspanspan-iddata_transferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>数据传输

X64 提供了可处理64位即时常量或内存地址的 MOV 指令的新变体。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r</strong>，#n</p></td>
<td align="left"><p><strong>r</strong> = #n</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>rax</strong>，m</p></td>
<td align="left"><p>将64位地址处的内容移动到 <strong>rax</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p>m、 <strong>rax</strong></p></td>
<td align="left"><p>将 <strong>rax</strong> 的内容移动到64位地址。</p></td>
</tr>
</tbody>
</table>

 

X64 还提供了一个新的指令，用于将32位操作数进行签名扩展到64位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVSXD</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>将带符号扩展的 DWORD 移到 QWORD。</p></td>
</tr>
</tbody>
</table>

 

到32位 subregisters 的普通 MOV 操作自动扩展到64位，因此没有 MOVZXD 指令。

可以使用两个 SSE 指令将128位 (值（如 Guid) 从内存移到一个 **xmm**_n_ 注册，反之亦然）。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVDQA</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m</p></td>
<td align="left"><p>将128位对齐值移动到 <strong>xmm</strong><em>n</em> register，反之亦然。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOVDQU</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m</p></td>
<td align="left"><p>将128位值 (不必与) 对齐，反之亦然。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddata_conversionspanspan-iddata_conversionspanspan-iddata_conversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>数据转换

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CDQE</p></td>
<td align="left"><p>将 dword (<strong>eax</strong>) 转换为 qword (<strong>rax</strong>) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CQO</p></td>
<td align="left"><p>将 qword (<strong>rax</strong>) 转换为 oword (<strong>rdx</strong>：<strong>rax</strong>) 。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idstring_manipulationspanspan-idstring_manipulationspanspan-idstring_manipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>字符串操作

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVSQ</p></td>
<td align="left"><p>将 qword 从 <strong>rsi</strong> 移动到 <strong>rdi.tpl。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>CMPSQ</p></td>
<td align="left"><p>将 <strong>rsi</strong> 与 rdi.tpl 进行比较 <strong>。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCASQ</p></td>
<td align="left"><p>在 <strong>rdi.tpl</strong>扫描 qword。 将 <strong>rdi.tpl</strong> 与 <strong>rax</strong>进行比较。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LODSQ</p></td>
<td align="left"><p>将 qword 从<strong>rsi</strong>加载到<strong>rax</strong>中<em>。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOSQ</p></td>
<td align="left"><p>将 qword 从<strong>rax</strong>存储到<strong>rdi.tpl</strong> <em>。</em></p></td>
</tr>
</tbody>
</table>

 

 

 





