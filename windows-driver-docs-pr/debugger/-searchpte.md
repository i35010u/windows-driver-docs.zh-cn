---
title: searchpte
description: Searchpte 扩展会搜索指定页面帧号 (PFN) 的物理内存。
keywords:
- searchpte Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- searchpte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fab1eb5c55ebcfe8265f26fe199b7114299ac3c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837567"
---
# <a name="searchpte"></a>!searchpte


**！ Searchpte** extension 搜索指定页面帧号 (PFN) 的物理内存。

```dbgcmd
!searchpte PFN 
!searchpte -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______PFN______"></span><span id="_______pfn______"></span>*PFN*   
以十六进制格式指定 PFN。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关页表和页目录的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

若要随时停止执行，请在 WinDbg) 中按 CTRL + BREAK (，或按 CTRL + C (KD) 。

 

 





