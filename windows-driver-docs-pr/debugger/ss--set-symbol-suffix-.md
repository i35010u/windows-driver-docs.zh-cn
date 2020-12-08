---
title: ss（设置符号后缀）
description: Ss 命令设置或显示用于数值表达式中的符号匹配的当前后缀值。
keywords:
- ss (设置) Windows 调试的符号后缀
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ss (Set Symbol Suffix)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1ef7ed6b63315d123d6d584e2e52af375e2d06c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836859"
---
# <a name="ss-set-symbol-suffix"></a>ss（设置符号后缀）


**Ss** 命令设置或显示用于数值表达式中的符号匹配的当前后缀值。

```dbgcmd
ss [a|w|n] 
```

## <a name="span-idddk_cmd_set_symbol_suffix_dbgspanspan-idddk_cmd_set_symbol_suffix_dbgspanparameters"></a><span id="ddk_cmd_set_symbol_suffix_dbg"></span><span id="DDK_CMD_SET_SYMBOL_SUFFIX_DBG"></span>参数


<span id="_______a______"></span><span id="_______A______"></span>**一个**   
指定符号后缀应为 "A"，匹配多个 ASCII 符号。

<span id="_______w______"></span><span id="_______W______"></span>**w**   
指定符号后缀应为 "W"，匹配许多 Unicode 符号。

<span id="_______n______"></span><span id="_______N______"></span>**n**   
指定调试器不应使用符号后缀。  (此参数是默认行为。 ) 

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关符号匹配的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

<a name="remarks"></a>备注
-------

如果将 **ss** 命令与 no 参数一起指定，则将显示后缀值的当前状态。

 

 





