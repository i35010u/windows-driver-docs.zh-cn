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
ms.openlocfilehash: 522016ebe465bb97d0820a615ccbf41049c83abb
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239488"
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

有关页表和页目录中的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

若要停止在任何时间执行，请按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD)。

 

 





