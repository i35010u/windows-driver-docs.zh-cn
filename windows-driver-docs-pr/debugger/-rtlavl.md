---
title: rtlavl
description: Rtlavl 扩展显示 RTL_AVL_TABLE 结构的条目。
ms.assetid: b1e19b13-8bb6-4f40-8d51-368fafc38ebc
keywords:
- avl 表
- rtlavl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rtlavl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 172382e4e4aadef1ec61372368a3489e92703bda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335693"
---
# <a name="rtlavl"></a>!rtlavl


**！ Rtlavl**扩展显示的是 RTL 条目\_AVL\_表结构。

```dbgcmd
!rtlavl Address [Module!Type]
!rtlavl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址的 RTL\_AVL\_表以显示。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定在其中定义数据结构的模块。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定数据结构的名称。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

使用[ **！ gentable** ](-gentable.md)扩展名，即可显示 AVL 表。

<a name="remarks"></a>备注
-------

其中包括<em>模块</em>**！**<em>类型</em>选项将导致每个条目中要解释为具有给定的类型的表。

通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （KD CDB） 中，可以在任何时间中断显示。

 

 





