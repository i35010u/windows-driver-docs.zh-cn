---
title: db、 dc、 dd、 dp、 dq、 du、 数据仓库
description: Db、 dc、 dd、 dp、 dq、 du 和 dw 扩展显示数据在目标计算机上指定的物理地址。
ms.assetid: d34eebb7-bc91-4bff-9787-d92f74195ee1
keywords:
- db 扩展插件
- dc 扩展
- dd 扩展
- 分发点扩展
- dq 扩展
- du 扩展
- dw 扩展
- 内存中，显示物理 (d) 扩展
- db、 dc、 dd、 dp、 dq、 du、 dw Windows 调试
ms.date: 01/18/2017
topic_type:
- apiref
api_name:
- db, dc, dd, dp, dq, du, dw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef7aeeb0f6597c7be3ae0e18c007e5dc7dd14fe8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336876"
---
# <a name="db-dc-dd-dp-dq-du-dw"></a>!db、!dc、!dd、!dp、!dq、!du、!dw


**！ Db**， **！ dc**， **！ dd**， **！ dp**， **！ dq**， **！ du**，和 **！ dw**扩展插件在目标计算机上指定的物理地址会显示数据。

不要将这些扩展命令与相混淆[ **d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令，或与[ **！ ntsdexts.dp** ](-dp---ntsdexts-dp-.md)扩展命令。

```dbgcmd
!db [Caching] [-m] [PhysicalAddress] [L Size] 
!dc [Caching] [-m] [PhysicalAddress] [L Size] 
!dd [Caching] [-m] [PhysicalAddress] [L Size] 
!dp [Caching] [-m] [PhysicalAddress] [L Size] 
!dq [Caching] [-m] [PhysicalAddress] [L Size] 
!du [Caching] [-m] [PhysicalAddress] [L Size] 
!dw [Caching] [-m] [PhysicalAddress] [L Size] 
```

## <a name="span-idddkddbgspanspan-idddkddbgspanparameters"></a><span id="ddk__d__dbg"></span><span id="DDK__D__DBG"></span>参数


<span id="_______Caching______"></span><span id="_______caching______"></span><span id="_______CACHING______"></span> *Caching*   
可以是以下值之一。 *Caching*值必须用方括号括起来：

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
将导致从内存缓存中读取此扩展。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
导致此扩展以读取未缓存的内存。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
导致此扩展以从写组合的内存中读取。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
会导致内存一次读取一个单位。 例如， **！ db-m**中读取 8 位块区中的内存和 **！ dw m**读取 16 位块中的内存。 如果您的硬件不支持 32 位的物理内存读取，可能需要使用 **-m**选项。 此选项不会影响的长度或显示的外观--它只影响访问内存的方式。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
指定要以十六进制格式显示的第一个物理地址。 如果省略第一次使用此命令，该地址默认为零。 如果省略此属性在后续使用，将最后一次显示结束的地方开始显示。

<span id="_______L_______Size______"></span><span id="_______l_______size______"></span><span id="_______L_______SIZE______"></span> **L** **** *大小*   
指定要显示的内存区块的数量。 块区大小由使用精确扩展名确定。

### <a name="span-iddllspanspan-iddllspanenvironment"></a><span id="DLL"></span><span id="dll"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式</p></td>
</tr>
</tbody>
</table>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要写入的物理内存，请使用[ **！ e\\**  * ](-eb---ed.md)扩展。 内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

每个这些扩展显示物理内存，但其显示格式和默认长度不同之处：

-   **！ Db**扩展显示十六进制字节和与其 ASCII 字符等效值。 默认长度为 128 个字节。

-   **！ Dc**扩展将 DWORD 值和其 ASCII 字符等效项显示。 默认长度为 32 的 dword 值 （128 总字节数）。

-   **！ Dd**扩展显示 DWORD 值。 默认长度为 32 的 dword 值 （128 总字节数）。

-   **！ Dp**扩展插件都会显示 ULONG\_PTR 值。 这些是 32 位或 64 位的单词，具体取决于指令大小。 默认长度为 128 的总字节数。

-   **！ Dq**扩展插件都会显示 ULONG64\_PTR 值。 这些是 32 位字。 默认长度为 128 的总字节数。

-   **！ Du**扩展显示 UNICODE 字符。 默认长度为 16 个字符 （32 总字节），或直到遇到 NULL 字符。

-   **！ Dw**扩展显示 WORD 值。 默认长度是 64 的 dword 值 （128 总字节数）。

因此，使用两个不同的值相同的这些扩展*大小*将最有可能结果中显示的内存总量存在差异。 例如，使用命令 **！ db L 32**结果中显示 （为十六进制字节为单位），32 个字节，而该命令 **！ dd L 32**结果中显示 （为 DWORD 值） 的 128 个字节。

下面是需要缓存的属性标志，在其中一个示例：

```dbgcmd
kd> !dc e9000
physical memory read at e9000 failed
If you know the caching attributes used for the memory,
try specifying [c], [uc] or [wc], as in !dd [c] <params>.
WARNING: Incorrect use of these flags will cause unpredictable
processor corruption. This may immediately (or at any time in
the future until reboot) result in a system hang, incorrect data
being displayed or other strange crashes and corruption.

kd> !dc [c] e9000
#   e9000 000ea002 000ea002 000ea002 000ea002 ................
#   e9010 000ea002 000ea002 000ea002 000ea002 ................
```

 

 





