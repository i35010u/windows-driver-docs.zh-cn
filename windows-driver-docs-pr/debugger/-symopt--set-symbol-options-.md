---
title: .symopt （设置符号选项）
description: .Symopt 命令设置或显示符号选项。
ms.assetid: 0793baa3-14f7-48df-8773-736b6a5470e6
keywords:
- .symopt （设置符号选项） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symopt (Set Symbol Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4654c414d39a4c213818d269c08653c03efb85a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554086"
---
# <a name="symopt-set-symbol-options"></a>.symopt （设置符号选项）


**.Symopt**命令设置或显示符号选项。

```dbgcmd
.symopt+ Flags 
.symopt- Flags 
.symopt 
```

## <a name="span-idddkmetasetsymboloptionsdbgspanspan-idddkmetasetsymboloptionsdbgspanparameters"></a><span id="ddk_meta_set_symbol_options_dbg"></span><span id="DDK_META_SET_SYMBOL_OPTIONS_DBG"></span>参数


<span id="______________"></span> **+**   
指定的符号选项将导致*标志*设置。 如果 **.symopt**用于*标志*，但任何加号或减号，假定一个加号。

<span id="_______-______"></span> **-**   
指定的符号选项将导致*标志*要清除。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要更改符号选项。 *标志*必须是这些符号选项的位标志的总和。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

列表和每个符号选项、 它的位标志和设置并清除这些选项的其他方法的说明，请参阅[设置符号选项](symbol-options.md)。

<a name="remarks"></a>备注
-------

不带任何参数， **.symopt**显示当前符号选项。

 

 





