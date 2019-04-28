---
title: .ofilter（筛选目标输出）
description: .Ofilter 命令筛选目标应用程序或目标计算机的输出。
ms.assetid: 0b94d177-0e41-4781-b0bc-ed58cee584f1
keywords:
- 筛选器目标输出 (.ofilter) 命令
- .ofilter （筛选器目标输出） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ofilter (Filter Target Output)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a677e282689a761b13b40abbaea4427de4a5d19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334428"
---
# <a name="ofilter-filter-target-output"></a>.ofilter（筛选目标输出）


**.Ofilter**命令筛选器的目标应用程序或目标计算机的输出。

```dbgcmd
.ofilter [/!] String 
.ofilter "" 
.ofilter 
```

## <a name="span-idddkmetafiltertargetoutputdbgspanspan-idddkmetafiltertargetoutputdbgspanparameters"></a><span id="ddk_meta_filter_target_output_dbg"></span><span id="DDK_META_FILTER_TARGET_OUTPUT_DBG"></span>参数


<span id="_______________"></span> **/!**   
反转该筛选器，以便调试器将显示不包含的仅限 output*字符串*。 如果不使用此参数，调试器将显示包含的仅限 output*字符串*。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
指定要匹配的目标输出中的字符串。 *字符串*可以包含空格，但不能使用 C 样式控制字符，例如 **\\"** 并 **\\n**。 *字符串*可能包含多个通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

您可以将*字符串*引号引起来。 但是，如果*字符串*包括一个分号，前导空格或尾随空格，则必须使用引号。 中的字母数字字符*字符串*是转换为大写的字母，但实际的模式匹配是不区分大小写。

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

有关详细信息[ **OutputDebugString** ](https://msdn.microsoft.com/library/windows/desktop/aa363362)和其他用户模式下例程，请参阅 Microsoft Windows SDK 文档。 有关详细信息**DbgPrint**， **DbgPrintEx**，和其他内核模式例程，请参阅 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

如果您使用 **.ofilter**命令不带参数，则调试器会显示当前的模式匹配条件。

若要清除现有的筛选器，请使用 **.ofilter""**。 此命令可以筛选由用户模式下例程发送任何数据 (如[ **OutputDebugString**](https://msdn.microsoft.com/library/windows/desktop/aa363362)) 和内核模式例程 (如**DbgPrint**)。 但是，调试器将始终显示提示， **DbgPrompt**发送。

**DbgPrintEx**并**KdPrintEx**例程提供筛选不希望的调试消息的另一种方法。

 

 





