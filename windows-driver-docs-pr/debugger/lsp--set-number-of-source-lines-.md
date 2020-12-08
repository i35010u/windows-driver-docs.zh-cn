---
title: lsp（设置源行数目）
description: Lsp 命令控制在单步执行或执行代码或使用 ls 和 lsa 命令时显示多少源行。
keywords:
- lsp (设置) Windows 调试的源行数
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsp (Set Number of Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c21dc06bb8c0076ece55055e113aa853ea6ca36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819157"
---
# <a name="lsp-set-number-of-source-lines"></a>lsp（设置源行数目）


**Lsp** 命令控制在单步执行或执行代码或使用 [**ls 和 lsa 命令**](ls--lsa--list-source-lines-.md)时显示多少源行。

```dbgcmd
lsp [-a] LeadingLines TrailingLines 
lsp [-a] TotalLines 
lsp [-a] 
```

## <a name="span-idddk_cmd_set_number_of_source_lines_dbgspanspan-idddk_cmd_set_number_of_source_lines_dbgspanparameters"></a><span id="ddk_cmd_set_number_of_source_lines_dbg"></span><span id="DDK_CMD_SET_NUMBER_OF_SOURCE_LINES_DBG"></span>参数


<span id="_______-a______"></span><span id="_______-A______"></span>**-a**   
设置或显示 **ls** 和 **lsa** 显示的行数。 如果省略 **-a**， **lsp** 将设置或显示在单步执行代码和执行代码时显示的行数。

<span id="_______LeadingLines______"></span><span id="_______leadinglines______"></span><span id="_______LEADINGLINES______"></span>*LeadingLines*   
指定要在当前行之前显示的行数。

<span id="_______TrailingLines______"></span><span id="_______trailinglines______"></span><span id="_______TRAILINGLINES______"></span>*TrailingLines*   
指定要在当前行之后显示的行数。

<span id="_______TotalLines______"></span><span id="_______totallines______"></span><span id="_______TOTALLINES______"></span>*TotalLines*   
指定要显示的总行数。 此数字均匀地分为前导和尾随直线。  (如果此数为奇数，则显示更多的尾随行。 ) 

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

如果在不使用任何参数的情况下使用 **lsp** 命令，则 **lsp** 将显示您在单步执行时使用的当前前导行和尾随行值。 如果将此命令与 **-a** 参数一起使用，则 **lsp** 将显示在单步执行和 [**ls 命令**](ls--lsa--list-source-lines-.md)时使用的值。

当你在程序执行后单步执行程序或中断时，以前的 **lsp** 命令将确定所显示的前导和尾随行的数目。 使用 **lsa** 时，以前的 **lsp-a** 命令确定所显示的前导和尾随行的数目。 使用 **ls** 时，所有行都显示为单个块，因此先前的 **lsp-a** 命令确定所显示的总行数。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源调试和相关命令的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。

 

 





