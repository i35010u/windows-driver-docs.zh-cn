---
title: x64 说明
description: x64 说明
ms.assetid: f05cbf3e-001c-43cc-8a53-0e22fd161a53
keywords:
- x64 处理器，说明
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 864abf8d4d44426f90f580b209b66e8fd78f3581
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554480"
---
# <a name="x64-instructions"></a>x64 说明


## <span id="ddk_x64_instructions_dbg"></span><span id="DDK_X64_INSTRUCTIONS_DBG"></span>


大多数 x86 说明仍可以在 64 位模式下有效的 x64。 某些很少使用的操作不再支持在 64 位模式下，例如：

-   二进制编码十进制算术说明：AAA、 AAD、 AAM、 AAS、 DAA、 DAS

-   绑定

-   PUSHAD 和 POPAD

-   处理段寄存器，如 DS PUSH 和 POP DS 的大多数操作。 （使用 FS 或 GS 段寄存器的操作是仍然有效。）

X64 指令集包括最近添加到 x86，如 SSE 2 的项目。 针对 x64 编译的程序可以自由地使用这些说明。

### <a name="span-iddatatransferspanspan-iddatatransferspanspan-iddatatransferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>数据传输

X64 提供 MOV 指令可处理 64 位即时常量或内存地址的新变体。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r</strong>,#n</p></td>
<td align="left"><p><strong>r</strong> = #n</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>到 rax</strong>，m</p></td>
<td align="left"><p>将内容移动到 64 位地址处<strong>rax</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p>m、 <strong>rax</strong></p></td>
<td align="left"><p>将内容移<strong>rax</strong>到 64 位地址。</p></td>
</tr>
</tbody>
</table>

 

X64 还提供了新的说明，以符号扩展为 64 位的 32 位操作数。

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
<td align="left"><p>将双字节带符号扩展移动到 QWORD。</p></td>
</tr>
</tbody>
</table>

 

32 位 subregisters 自动零到普通 MOV 操作扩展为 64 位，因此没有任何 MOVZXD 指令。

两个 SSE 指令可用于从内存移动 128 位值 （如 Guid) **xmm * * * n*寄存器，反之亦然。

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
<td align="left"><p>移动到的 128 位对齐的值<strong>xmm</strong><em>n</em>注册，反之亦然。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOVDQU</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m</p></td>
<td align="left"><p>移动 128 位值 （不一定是对齐） 若要注册，反之亦然。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddataconversionspanspan-iddataconversionspanspan-iddataconversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>数据转换

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CDQE</p></td>
<td align="left"><p>转换 dword (<strong>eax</strong>) 到 qword (<strong>rax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CQO</p></td>
<td align="left"><p>转换 qword (<strong>rax</strong>) 到 oword (<strong>rdx</strong>:<strong>rax</strong>)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idstringmanipulationspanspan-idstringmanipulationspanspan-idstringmanipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>字符串操作

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVSQ</p></td>
<td align="left"><p>移动从 qword <strong>rsi</strong>到<strong>rdi。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>CMPSQ</p></td>
<td align="left"><p>比较在 qword <strong>rsi</strong>与<strong>rdi。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCASQ</p></td>
<td align="left"><p>扫描在 qword <strong>rdi</strong>。 比较在 qword <strong>rdi</strong>到<strong>rax</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LODSQ</p></td>
<td align="left"><p>加载从 qword <strong>rsi</strong>成<strong>rax</strong><em>。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOSQ</p></td>
<td align="left"><p>存储到 qword <strong>rdi</strong>从<strong>rax</strong><em>。</em></p></td>
</tr>
</tbody>
</table>

 

 

 





