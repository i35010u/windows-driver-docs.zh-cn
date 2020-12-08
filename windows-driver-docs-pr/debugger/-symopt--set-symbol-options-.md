---
title: .symopt（设置符号选项）
description: Symopt 命令设置或显示符号选项。
keywords:
- symopt (设置) Windows 调试的符号选项
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symopt (Set Symbol Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2ad4a842b4ad38b3d7987a688179e0d9a68106f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832019"
---
# <a name="symopt-set-symbol-options"></a>.symopt（设置符号选项）


**Symopt** 命令设置或显示符号选项。

```dbgcmd
.symopt+ Flags 
.symopt- Flags 
.symopt 
```

## <a name="span-idddk_meta_set_symbol_options_dbgspanspan-idddk_meta_set_symbol_options_dbgspanparameters"></a><span id="ddk_meta_set_symbol_options_dbg"></span><span id="DDK_META_SET_SYMBOL_OPTIONS_DBG"></span>参数


<span id="______________"></span> **+**   
导致设置由 *标志* 指定的符号选项。 如果将 **. symopt** 与 *标志* 一起使用，但不使用加号或减号，则假定使用了正负号。

<span id="_______-______"></span> **-**   
导致清除 *标志* 指定的符号选项。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要更改的符号选项。 *Flags* 必须是这些符号选项的位标志之和。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关每个符号选项的列表和说明、其位标志以及其他设置和清除这些选项的方法，请参阅 [设置符号选项](symbol-options.md)。

<a name="remarks"></a>备注
-------

如果没有任何参数， **. symopt** 将显示当前的符号选项。

 

 





