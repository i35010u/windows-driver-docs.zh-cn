---
title: db，dc，dd，dp，dq，du，dw
description: Db、dc、dd、dp、dq、du 和 dw 扩展显示目标计算机上指定物理地址的数据。
keywords:
- db 扩展
- dc 扩展
- dd 扩展
- dp 扩展
- dq 扩展
- du 扩展
- dw 扩展
- 内存，显示物理 ( d ) 扩展
- db，dc，dd，dp，dq，du，dw Windows 调试
ms.date: 01/18/2017
topic_type:
- apiref
api_name:
- db, dc, dd, dp, dq, du, dw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 264d2de97dc85edfc7718f32e9f96c5578525600
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792065"
---
# <a name="db-dc-dd-dp-dq-du-dw"></a>!db、!dc、!dd、!dp、!dq、!du、!dw


**！ Db**， **！ dc**， **！ dd**， **！ dp**， **！ dq**， **！ du** 和 **！ dw** 扩展在目标计算机上的指定物理地址显示数据。

不应将这些扩展命令与 [**d \* (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令或与 [**！ ntsdexts**](-dp---ntsdexts-dp-.md) extension 命令混淆。

```dbgcmd
!db [Caching] [-m] [PhysicalAddress] [L Size] 
!dc [Caching] [-m] [PhysicalAddress] [L Size] 
!dd [Caching] [-m] [PhysicalAddress] [L Size] 
!dp [Caching] [-m] [PhysicalAddress] [L Size] 
!dq [Caching] [-m] [PhysicalAddress] [L Size] 
!du [Caching] [-m] [PhysicalAddress] [L Size] 
!dw [Caching] [-m] [PhysicalAddress] [L Size] 
```

## <a name="span-idddk__d__dbgspanspan-idddk__d__dbgspanparameters"></a><span id="ddk__d__dbg"></span><span id="DDK__D__DBG"></span>参数


<span id="_______Caching______"></span><span id="_______caching______"></span><span id="_______CACHING______"></span>*缓存*   
可以是下列值之一。 *缓存* 值必须用方括号括起来：

<span id="_c_"></span><span id="_C_"></span>**\[ansi-c\]**  
使此扩展从缓存的内存中读取。

<span id="_uc_"></span><span id="_UC_"></span>**\[通信\]**  
使此扩展从未缓存的内存中读取。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc.exe\]**  
使此扩展读取写入合并内存。

<span id="_______-m______"></span><span id="_______-M______"></span>**-m**   
导致内存一次读取一个单元。 例如， **！ db-library** 读取8位区块中的内存，而 **！ dw-m** 读取16位区块中的内存。 如果你的硬件不支持32位物理内存读取，则可能需要使用 **-m** 选项。 此选项不会影响显示器的长度或外观，只会影响对内存的访问方式。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
以十六进制格式指定要显示的第一个物理地址。 如果在第一次使用此命令时省略此值，则地址默认为零。 如果在后续使用时省略此情况，则会在最后一次显示结束的位置开始显示。

<span id="_______L_______Size______"></span><span id="_______l_______size______"></span><span id="_______L_______SIZE______"></span>**L**  **** *大小*   
指定要显示的内存块的数量。 块区的大小由使用的精确扩展决定。

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


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要写入物理内存，请使用 [ **！ e \\** _](-eb---ed.md)扩展。 有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

每个扩展都显示物理内存，但其显示格式和默认长度不同：

-   _ *！ Db** 扩展显示十六进制字节及其等效的 ASCII 字符。 默认长度为128个字节。

-   **！ Dc** 扩展显示 DWORD 值及其等效的 ASCII 字符。 默认长度为 32 Dword (128 total bytes) 。

-   **！ Dd** 扩展显示 DWORD 值。 默认长度为 32 Dword (128 total bytes) 。

-   **！ Dp** 扩展显示 ULONG \_ PTR 值。 它们为32位或64位词，具体取决于指令大小。 默认长度为128个字节。

-   **！ Dq** 扩展显示 ULONG64 \_ PTR 值。 这些是32位词。 默认长度为128个字节。

-   **！ Du** EXTENSION 显示 UNICODE 字符。 默认长度为16个字符 (32) 总字节数，或在遇到 NULL 字符之前。

-   **！ Dw** 扩展显示字值。 默认长度为 64 Dword (128 total bytes) 。

因此，使用与相同 *大小* 值不同的其中两个扩展时，很有可能会导致显示的内存总量有差异。 例如，使用命令 **！ Db L 32** 将以十六进制字节的形式 (显示32字节) ，而命令 **！ dd L 32** 会导致128字节显示 (为 DWORD 值) 。

下面是需要缓存特性标志的示例：

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

 

 





