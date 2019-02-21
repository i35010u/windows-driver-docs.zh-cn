---
title: eb ed
description: Eb 和 ed 扩展写入指定的物理地址的一系列值。 这些扩展命令不应混淆和 e\\ （输入值） 命令。
ms.assetid: 368937e4-0989-4dca-983a-65bc63142108
keywords:
- eb 扩展
- ed 扩展
- 内存中，物理写入 (e) 扩展
- eb，ed Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- eb, ed
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec85a19cf391ba5831c813b1749e6ffe0bbeb695
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522214"
---
# <a name="eb-ed"></a>！ eb，！ ed


**！ Eb**并 **！ ed**扩展将一系列值写入到指定的物理地址。

不要将这些扩展命令与相混淆[ **e\* （输入值）** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令。

```dbgcmd
!eb [Flag] PhysicalAddress Data [ ... ] 
!ed [Flag] PhysicalAddress Data [ ... ]
```

## <a name="span-idddkedbgspanspan-idddkedbgspanparameters"></a><span id="ddk__e__dbg"></span><span id="DDK__E__DBG"></span>参数


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *Flag*   
可以是以下值之一。 *标志*值必须用方括号括起来：

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
写入内存缓存。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
将写入到未缓存的内存。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
写入写组合内存。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
指定数据将写入，以十六进制格式的目标计算机上的第一个物理地址。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *数据*   
指定一个或多个值按顺序写入到的物理内存。 以十六进制格式输入这些值。 有关 **！ eb**扩展中，每个值必须是 1 个字节 （两个十六进制数字）。 有关 **！ ed**扩展中，每个值必须是一个 DWORD （八个十六进制数字）。 可以包含任意数量的*数据*上一行的值。 若要分隔多个值，请使用逗号或空格。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要读取的物理内存，使用[ **！ d\\**  * ](-db---dc---dd---dp---dq---du---dw.md)扩展。 内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

 

 





