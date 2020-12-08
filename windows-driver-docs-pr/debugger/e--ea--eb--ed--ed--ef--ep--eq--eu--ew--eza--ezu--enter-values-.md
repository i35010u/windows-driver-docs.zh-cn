---
title: 'e，ea，eb，ed，eD，ef，ep，eq，eu，new，eza (输入值) '
description: E * 命令在内存中输入指定的值。不应将此命令与 ~ E (线程特定命令) 限定符混淆。
keywords:
- e，ea，eb，ed，eD，ef，ep，eq，eu，eza (输入值) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- e, ea, eb, ed, eD, ef, ep, eq, eu, ew, eza (Enter Values)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76110e2a4eb994272f6ac2e378ada7c622b170fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838653"
---
# <a name="e-ea-eb-ed-ed-ef-ep-eq-eu-ew-eza-enter-values"></a>e，ea，eb，ed，eD，ef，ep，eq，eu，new，eza (输入值) 


**E \\** _ 命令在内存中输入指定的值。

此命令不应与 [_ *~ E (线程特定的命令)* *](-e--thread-specific-command-.md)限定符混淆。

```dbgcmd
e{b|d|D|f|p|q|w} Address [Values] 
e{a|u|za|zu} Address "String" 
e Address [Values]
```

## <a name="span-idddk_cmd_enter_values_dbgspanspan-idddk_cmd_enter_values_dbgspanparameters"></a><span id="ddk_cmd_enter_values_dbg"></span><span id="DDK_CMD_ENTER_VALUES_DBG"></span>参数


### <a name="span-idsyntax__ed_efspanspan-idsyntax__ed_efspansyntax-ed-ef"></a><span id="syntax__ed_ef"></span><span id="SYNTAX__ED_EF"></span>语法 eD ef

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定输入值的起始地址。 调试器替换 *Address* 和每个后续内存位置上的值，直到使用了所有 *值* 。

<span id="_______Values______"></span><span id="_______values______"></span><span id="_______VALUES______"></span>*值*   
指定要输入到内存中的一个或多个值。 多个数值应该用空格分隔。 如果未指定任何值，则将显示当前地址和该地址处的值，并且系统将提示您输入。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
指定要输入到内存中的字符串。 **Ea** 和 **eza** 命令会将此作为 ASCII 字符串写入内存;**欧盟** 和 **ezu** 命令会将此作为 Unicode 字符串写入内存。 **Eza** 和 **ezu** 命令写入终端 **NULL**;**ea** 和 **欧盟** 命令没有。 *字符串* 必须用引号引起来。

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

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

此命令采用以下形式存在。 **Ed** 和 **ed** 命令的第二个字符区分大小写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">Enter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>这将以与最近的 e 命令相同的格式输入数据 <strong> <em> </strong> 。  (如果最近的 <strong> e </em></strong> 命令为 <strong>ea</strong>、 <strong>eza</strong>、 <strong>eu</strong>或 <strong>ezu</strong>，则最终参数将是 <em>字符串</em> ，不能省略。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>中文</strong></p></td>
<td align="left"><p>不以 NULL 结尾的 ASCII 字符串 () 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eb</strong></p></td>
<td align="left"><p>字节值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ed-24000b</strong></p></td>
<td align="left"><p>双字值 (4 个字节) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Ed-24000b</strong></p></td>
<td align="left"><p>双精度浮点数字 (8 字节) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ef</strong></p></td>
<td align="left"><p>单精度浮点数字 (4 个字节) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ep</strong></p></td>
<td align="left"><p>指针大小的值。 此命令等效于 <strong>ed</strong> 或 <strong>eq</strong>，具体取决于目标计算机的处理器体系结构是否分别为32位或64位。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eq</strong></p></td>
<td align="left"><p>四字值 (8 字节) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eu</strong></p></td>
<td align="left"><p>Unicode 字符串 (非 NULL 终止的) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>new</strong></p></td>
<td align="left"><p>字值 (2 个字节) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eza</strong></p></td>
<td align="left"><p>以 NULL 结尾的 ASCII 字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ezu</strong></p></td>
<td align="left"><p>以 NULL 结尾的 Unicode 字符串。</p></td>
</tr>
</tbody>
</table>

 

数值将被解释为当前基数 (16、10或 8) 中的数字。 若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。 可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来替代默认基数。

**注意**   使用 c + + 表达式时，默认基数的行为会有所不同。 有关详细信息，请参阅 [计算表达式](evaluating-expressions.md) 。

 

使用 **eb** 命令输入字节值时，可以使用直引号指定字符。 如果要包含多个字符，则每个字符必须用其自己的引号括起来。 这允许您输入一个不是以 null 字符结尾的字符字符串。 例如：

```dbgcmd
eb 'h' 'e' 'l' 'l' 'o'
```

C 样式转义符 (如 " \\ 0" 或 " \\ n" ) 不能与这些命令一起使用。

如果省略 *Values* 参数，系统会提示输入。 将显示地址及其当前内容，并将显示 **输入 &gt;** 提示。 然后，可以执行以下任一操作：

-   输入一个新值，然后按 ENTER。

-   按下空格后跟 ENTER，保留内存中的当前值。

-   按 ENTER 退出命令。

 

 





