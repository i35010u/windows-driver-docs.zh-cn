---
title: .fnent （显示函数的数据）
description: .Fnent 命令显示有关指定的函数的函数表项的信息。
ms.assetid: 914caf55-2fbf-4f30-af6e-e666dc47c7da
keywords:
- 显示函数的数据 (.fnent) 命令
- .fnent （显示函数的数据） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnent (Display Function Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22385219eaa6914c6561e6ce3acf0d6186d8075b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521470"
---
# <a name="fnent-display-function-data"></a>.fnent （显示函数的数据）


**.Fnent**命令显示有关指定的函数的函数表项的信息。

```dbgcmd
.fnent Address
```

## <a name="span-idddkmetadisplayfunctiondatadbgspanspan-idddkmetadisplayfunctiondatadbgspanparameters"></a><span id="ddk_meta_display_function_data_dbg"></span><span id="DDK_META_DISPLAY_FUNCTION_DATA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定函数的地址。

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

 

<a name="remarks"></a>备注
-------

符号搜索算法 **.fnent**命令是与相同[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令。 屏幕将首先显示最接近的符号。 然后，调试器将显示这些符号的第一个函数入口。

如果最近的符号不是函数表中，将不显示任何信息。

下面的示例显示了可能的显示。

```dbgcmd
0:001> .fnent 77f9f9e7
Debugger function entry 00b61f50 for:
(77f9f9e7)   ntdll!RtlpBreakWithStatusInstruction   |  (77f9fa98)   ntdll!DbgPrintReturnControlC

Params:    1
Locals:    0
Registers: 0

0:001> .fnent 77f9fa98
Debugger function entry 00b61f70 for:
(77f9fa98)   ntdll!DbgPrintReturnControlC   |  (77f9fb21)   ntdll!DbgPrompt

Non-FPO

0:001> .fnent 01005a60
No function entry for 01005a60
```

 

 





