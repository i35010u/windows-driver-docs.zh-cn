---
title: ss （设置符号后缀）
description: Ss 命令设置或显示当前用于符号数值表达式中匹配的后缀值。
ms.assetid: acf4cf2e-5b09-4d46-aa42-e539ee968685
keywords:
- ss （设置符号后缀） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ss (Set Symbol Suffix)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c230128657006ddbaa3d1504fe8c88515e6d6e3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526174"
---
# <a name="ss-set-symbol-suffix"></a>ss （设置符号后缀）


**Ss**命令设置或显示当前用于符号数值表达式中匹配的后缀值。

```dbgcmd
ss [a|w|n] 
```

## <a name="span-idddkcmdsetsymbolsuffixdbgspanspan-idddkcmdsetsymbolsuffixdbgspanparameters"></a><span id="ddk_cmd_set_symbol_suffix_dbg"></span><span id="DDK_CMD_SET_SYMBOL_SUFFIX_DBG"></span>参数


<span id="_______a______"></span><span id="_______A______"></span> **a**   
指定符号后缀应为"A"匹配的许多 ASCII 符号。

<span id="_______w______"></span><span id="_______W______"></span> **w**   
指定符号后缀应为"W"，以匹配 Unicode 符号多。

<span id="_______n______"></span><span id="_______N______"></span> **n**   
指定调试程序不应使用符号后缀。 （此参数是默认行为。）

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

有关匹配的符号的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

<a name="remarks"></a>备注
-------

如果指定**ss**命令没有参数，以及显示后缀值的当前状态。

 

 





