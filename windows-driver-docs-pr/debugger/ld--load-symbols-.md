---
title: ld（加载符号）
description: Ld 命令为指定的模块加载符号并更新所有模块信息。
keywords:
- ld (加载符号) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ld (Load Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 798d206f357ed90841ae8434552cd76f87d88652
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806519"
---
# <a name="ld-load-symbols"></a>ld（加载符号）


**Ld** 命令为指定的模块加载符号并更新所有模块信息。

```dbgcmd
ld ModuleName [/f FileName]
```

## <a name="span-idddk_cmd_load_symbols_dbgspanspan-idddk_cmd_load_symbols_dbgspanparameters"></a><span id="ddk_cmd_load_symbols_dbg"></span><span id="DDK_CMD_LOAD_SYMBOLS_DBG"></span>参数


<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span>*ModuleName*   
指定要加载其符号的模块的名称。 *ModuleName* 可以包含各种通配符和说明符。

<span id="________f_______FileName______"></span><span id="________f_______filename______"></span><span id="________F_______FILENAME______"></span>**/F** *FileName*   
更改为匹配项选择的名称。 默认情况下，模块名称是匹配的，但使用 **/f** 时，文件名是匹配的，而不是模块名称。 *文件名* 可以包含各种通配符和说明符。 有关通配符和说明符语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

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

调试器的默认行为是使用 *延迟符号加载* (也称为 [延迟符号加载](deferred-symbol-loading.md)) 。 这意味着在需要符号之前，不会实际加载符号。

另一方面， **ld** 命令强制加载指定模块的所有符号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关延迟 (延迟) 符号加载的详细信息，请参阅 [延迟符号加载](deferred-symbol-loading.md)。 有关其他符号选项的详细信息，请参阅 [设置符号选项](symbol-options.md)。

 

 





