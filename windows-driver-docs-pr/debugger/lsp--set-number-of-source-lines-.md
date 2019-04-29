---
title: lsp（设置源行数目）
description: Lsp 命令控制单步执行或执行代码或使用 ls 和 lsa 命令时显示源行数。
ms.assetid: 350933f1-5459-4ba2-9ca7-a42341cf95de
keywords:
- lsp （设置源行数） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsp (Set Number of Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3350405a16da2b9fb75e8f41f73ae1c48e902897
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383312"
---
# <a name="lsp-set-number-of-source-lines"></a>lsp（设置源行数目）


**Lsp**命令控制单步执行时显示或执行代码或使用的源行数[ **ls 和 lsa 命令**](ls--lsa--list-source-lines-.md)。

```dbgcmd
lsp [-a] LeadingLines TrailingLines 
lsp [-a] TotalLines 
lsp [-a] 
```

## <a name="span-idddkcmdsetnumberofsourcelinesdbgspanspan-idddkcmdsetnumberofsourcelinesdbgspanparameters"></a><span id="ddk_cmd_set_number_of_source_lines_dbg"></span><span id="DDK_CMD_SET_NUMBER_OF_SOURCE_LINES_DBG"></span>参数


<span id="_______-a______"></span><span id="_______-A______"></span> **-a**   
设置或显示的行数的**ls**并**lsa**显示。 如果省略 **-a**， **lsp**设置或显示在单步执行和执行代码时显示的行数。

<span id="_______LeadingLines______"></span><span id="_______leadinglines______"></span><span id="_______LEADINGLINES______"></span> *LeadingLines*   
指定要在当前行之前显示行的数。

<span id="_______TrailingLines______"></span><span id="_______trailinglines______"></span><span id="_______TRAILINGLINES______"></span> *TrailingLines*   
指定要显示在当前行之后的行数。

<span id="_______TotalLines______"></span><span id="_______totallines______"></span><span id="_______TOTALLINES______"></span> *TotalLines*   
指定要显示的行的总数。 此数字是前导空格和尾随行之间平均划分。 （如果此数字为奇数，更多的尾随行显示。）

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

当你使用**lsp**命令及任何参数**lsp**显示当前的前导行和尾随单步执行时使用的行值。 当使用此命令和唯一 **-a**参数， **lsp**用于时单步执行和的值将显示[ **ls 和 lsa 命令**](ls--lsa--list-source-lines-.md).

当你单步执行程序或中断后执行程序、 上一张**lsp**命令确定的前导空格和尾随显示的行数。 当你使用**lsa**，以前**lsp-a**命令确定的前导空格和尾随显示的行数。 当你使用**ls**，所有行都显示为单个块中，因此前面**lsp-a**命令确定所显示的行总数。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关源调试相关的命令的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

 

 





