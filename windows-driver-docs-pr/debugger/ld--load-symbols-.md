---
title: ld（加载符号）
description: Ld 命令加载指定的模块的符号和更新模块的所有信息。
ms.assetid: 1dae519f-8dd1-4f30-98f4-fe904454c84c
keywords:
- ld （加载符号） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ld (Load Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 606e10615b5c49e421f448d95991d0ad77956578
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383514"
---
# <a name="ld-load-symbols"></a>ld（加载符号）


**Ld**命令加载指定的模块的符号和更新模块的所有信息。

```dbgcmd
ld ModuleName [/f FileName]
```

## <a name="span-idddkcmdloadsymbolsdbgspanspan-idddkcmdloadsymbolsdbgspanparameters"></a><span id="ddk_cmd_load_symbols_dbg"></span><span id="DDK_CMD_LOAD_SYMBOLS_DBG"></span>参数


<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span> *ModuleName*   
指定要加载其符号的模块的名称。 *ModuleName*可以包含各种通配符和说明符。

<span id="________f_______FileName______"></span><span id="________f_______filename______"></span><span id="________F_______FILENAME______"></span> **/f** *FileName*   
更改所选匹配项的名称。 默认情况下的模块名称匹配，但是当 **/f**使用而不是模块名称匹配的文件的名称。 *文件名*可以包含各种通配符和说明符。 有关语法的通配符字符和说明符的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

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

调试器的默认行为是使用*延迟符号加载*(也称为[延迟的符号加载](deferred-symbol-loading.md))。 这意味着，符号才会真正加载需要使用它们。

**Ld**命令，但是，将强制所有指定的模块加载符号。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关延迟 （延迟） 符号加载详细信息，请参阅[推迟符号加载](deferred-symbol-loading.md)。 有关其他符号选项的详细信息，请参阅[设置符号选项](symbol-options.md)。

 

 





