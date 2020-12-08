---
title: eb，ed
description: Eb 和 ed 扩展将值序列写入指定的物理地址。 不应将这些扩展命令与 e \\ () 命令输入值混淆。
keywords:
- eb 扩展
- ed 扩展
- 内存，写入物理 ( e ) 扩展
- eb，ed Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- eb, ed
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3336107cd7d30224d701b299cfb6f5d3eb113d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799885"
---
# <a name="eb-ed"></a>!eb、!ed


**！ Eb** 和 **！ ed** 扩展将值序列写入指定的物理地址。

不应将这些扩展命令与 [**e \* () 命令输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md) 混淆。

```dbgcmd
!eb [Flag] PhysicalAddress Data [ ... ] 
!ed [Flag] PhysicalAddress Data [ ... ]
```

## <a name="span-idddk__e__dbgspanspan-idddk__e__dbgspanparameters"></a><span id="ddk__e__dbg"></span><span id="DDK__E__DBG"></span>参数


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
可以是下列值之一。 *标志* 值必须用方括号括起来：

<span id="_c_"></span><span id="_C_"></span>**\[ansi-c\]**  
写入缓存内存。

<span id="_uc_"></span><span id="_UC_"></span>**\[通信\]**  
写入未缓存的内存。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc.exe\]**  
写入写入合并内存。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
指定要将数据写入到的目标计算机上的第一个物理地址（以十六进制表示）。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span>*数据*   
指定要按顺序写入物理内存中的一个或多个值。 以十六进制格式输入这些值。 对于 **！ eb** 扩展，每个值都必须为1个字节 (两个十六进制数字) 。 对于 **！ ed** 扩展，每个值都必须是一个 DWORD (8 个十六进制数字) 。 可以在一行中包含任意数量的 *数据* 值。 若要分隔多个值，请使用逗号或空格。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要读取物理内存，请使用 [ **！ \\ d** *](-db---dc---dd---dp---dq---du---dw.md)扩展。 有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

 

 





