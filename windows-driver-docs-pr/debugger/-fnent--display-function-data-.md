---
title: .fnent（显示函数数据）
description: Fnent 命令显示有关指定函数的函数表项的信息。
keywords:
- " () 命令显示函数数据"
- fnent (显示) Windows 调试的函数数据
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnent (Display Function Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0301d56f81e99397e05f4ad7068d49fd7517da1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815531"
---
# <a name="fnent-display-function-data"></a>.fnent（显示函数数据）


**Fnent** 命令显示有关指定函数的函数表项的信息。

```dbgcmd
.fnent Address
```

## <a name="span-idddk_meta_display_function_data_dbgspanspan-idddk_meta_display_function_data_dbgspanparameters"></a><span id="ddk_meta_display_function_data_dbg"></span><span id="DDK_META_DISPLAY_FUNCTION_DATA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定函数的地址。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**. Fnent** 命令的符号搜索算法与 [**Ln (列出最接近符号)**](ln--list-nearest-symbols-.md)命令相同。 首先显示最近的符号。 然后，调试器将显示其中第一个符号的函数条目。

如果函数表中不存在最近的符号，则不会显示任何信息。

下面的示例演示了可能的显示。

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

 

 





