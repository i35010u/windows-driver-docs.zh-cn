---
title: .ofilter（筛选目标输出）
description: Ofilter 命令筛选目标应用程序或目标计算机的输出。
ms.assetid: 0b94d177-0e41-4781-b0bc-ed58cee584f1
keywords:
- 筛选目标输出 ( ofilter) 命令
- ofilter (筛选器目标输出) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ofilter (Filter Target Output)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e5090817ff0bc448236b6305139f6ecc9d299d8
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716850"
---
# <a name="ofilter-filter-target-output"></a>.ofilter（筛选目标输出）


**Ofilter**命令筛选目标应用程序或目标计算机的输出。

```dbgcmd
.ofilter [/!] String 
.ofilter "" 
.ofilter 
```

## <a name="span-idddk_meta_filter_target_output_dbgspanspan-idddk_meta_filter_target_output_dbgspanparameters"></a><span id="ddk_meta_filter_target_output_dbg"></span><span id="DDK_META_FILTER_TARGET_OUTPUT_DBG"></span>参数


<span id="_______________"></span> **/!**   
反转筛选器，使调试器只显示不包含 *字符串*的输出。 如果不使用此参数，则调试器只显示包含 *字符串*的输出。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
指定目标的输出中要匹配的字符串。 *字符串*可以包括空格，但不能使用 C 样式控制字符，例如 "和** \\ n** ** \\ "** 。 *字符串* 可能包含各种通配符和说明符。 有关语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

可以用引号将 *字符串* 引起来。 但是，如果 *字符串* 包含分号、前导空格或尾随空格，则必须使用引号。 *字符串*中的字母数字字符转换为大写字母，但实际的模式匹配不区分大小写。

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

有关 [**OutputDebugString**](/windows/win32/api/debugapi/nf-debugapi-outputdebugstringw) 和其他用户模式例程的详细信息，请参阅 Microsoft Windows SDK 文档。 有关 **DbgPrint**、 **DbgPrintEx**和其他内核模式例程的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 。

<a name="remarks"></a>备注
-------

如果使用不带参数的 **ofilter** 命令，则调试器会显示当前的模式匹配条件。

若要清除现有筛选器，请使用 **ofilter ""**。 此命令对用户模式例程发送的任何数据进行筛选 (例如 [**OutputDebugString**](/windows/win32/api/debugapi/nf-debugapi-outputdebugstringw)) 和内核模式例程 (如 **DbgPrint**) 。 但是，调试器始终显示 **DbgPrompt** 发送的提示。

**DbgPrintEx**和**KdPrintEx**例程提供另一种筛选不需要的调试消息的方法。

 

