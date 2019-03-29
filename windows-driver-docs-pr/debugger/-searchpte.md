---
title: searchpte
description: Searchpte 扩展搜索物理内存分配给指定的页帧数 (PFN)。
ms.assetid: b9bac11e-605b-4064-b078-d3171b59da3b
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
ms.openlocfilehash: 954c895069cf8be024003b9ce39bf3b2adbacb75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567326"
---
# <a name="searchpte"></a>!searchpte


**！ Searchpte**扩展搜索物理内存分配给指定的页帧数 (PFN)。

```dbgcmd
!searchpte PFN 
!searchpte -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______PFN______"></span><span id="_______pfn______"></span> *PFN*   
以十六进制格式指定 PFN。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关页表和页目录中的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这本书不可能在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

若要停止在任何时间执行，请按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD)。

 

 





