---
title: 电子、 ea、 eb、 ed、 eD、 ef、 ep、 eq、 欧盟、 的新增功能，eza （输入值）
description: E * 命令输入到内存中指定的值。此命令不应混淆和 ~ E （特定于线程的命令） 限定符。
ms.assetid: d21b13ac-2268-4218-b562-4c466956b05d
keywords:
- 电子、 ea、 eb、 ed、 eD、 ef、 ep、 eq、 欧盟、 的新增功能、 eza （输入值） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- e, ea, eb, ed, eD, ef, ep, eq, eu, ew, eza (Enter Values)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f6d3ea07a9370798d35c9099ac3837a7b917b23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348479"
---
# <a name="e-ea-eb-ed-ed-ef-ep-eq-eu-ew-eza-enter-values"></a>电子、 ea、 eb、 ed、 eD、 ef、 ep、 eq、 欧盟、 的新增功能，eza （输入值）


**E\\*** 命令输入到内存中指定的值。

不要将此命令使用相混淆[ **~ E （特定于线程的命令）** ](-e--thread-specific-command-.md)限定符。

```dbgcmd
e{b|d|D|f|p|q|w} Address [Values] 
e{a|u|za|zu} Address "String" 
e Address [Values]
```

## <a name="span-idddkcmdentervaluesdbgspanspan-idddkcmdentervaluesdbgspanparameters"></a><span id="ddk_cmd_enter_values_dbg"></span><span id="DDK_CMD_ENTER_VALUES_DBG"></span>参数


### <a name="span-idsyntaxedefspanspan-idsyntaxedefspansyntax-ed-ef"></a><span id="syntax__ed_ef"></span><span id="SYNTAX__ED_EF"></span>语法 eD ef

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的起始地址输入值的位置。 调试器将处的值替换*地址*和每个后续的内存位置，直至将所有*值*已使用。

<span id="_______Values______"></span><span id="_______values______"></span><span id="_______VALUES______"></span> *值*   
指定一个或多个值输入到内存中。 应该用空格分隔多个数字值。 如果未指定任何值，将显示当前地址和该地址处的值，并且系统将提示你输入。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
指定要输入到内存中的字符串。 **Ea**并**eza**命令会将此作为 ASCII 字符串; 对内存**欧洲**并**ezu**命令会将此作为对内存Unicode 字符串。 **Eza**并**ezu**命令编写终端**NULL**; **ea**并**欧洲**命令不这样做。 *字符串*必须括在引号中。

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

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

此命令采用以下形式存在。 第二个字符**ed**并**eD**命令是区分大小写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">Enter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>这与最新相同的格式中输入数据<strong>e<em> </strong>命令。 (如果最新<strong>电子</em></strong>命令已<strong>ea</strong>， <strong>eza</strong>，<strong>欧洲</strong>，或<strong>ezu</strong>，最后一个参数将为<em>字符串</em>和不能省略。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ea</strong></p></td>
<td align="left"><p>ASCII 字符串 （不以 NULL 终止）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eb</strong></p></td>
<td align="left"><p>字节值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ed</strong></p></td>
<td align="left"><p>双字值 （4 个字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eD</strong></p></td>
<td align="left"><p>双精度浮点数 （8 字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ef</strong></p></td>
<td align="left"><p>单精度浮点数 （4 个字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ep</strong></p></td>
<td align="left"><p>指针大小值。 此命令是等效于<strong>ed</strong>或<strong>eq</strong>，具体取决于目标计算机的处理器体系结构是否 32 位或 64 位分别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eq</strong></p></td>
<td align="left"><p>四字值 （8 字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eu</strong></p></td>
<td align="left"><p>Unicode 字符串 （不以 NULL 终止）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ew</strong></p></td>
<td align="left"><p>字值 （2 个字节）。</p></td>
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

 

数字值将被解释为当前基数 （16、 10 或 8） 中的数字。 若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。

**请注意**  的默认基数以不同方式行为时C++使用表达式。 请参阅[评估表达式](evaluating-expressions.md)有关详细信息。

 

输入字节的值时**eb**命令时，可以使用直单引号来指定字符。 如果你想要包括多个字符，每个必须加上其自己的引号括起来。 这允许您输入未终止的 null 字符的字符串。 例如：

```dbgcmd
eb 'h' 'e' 'l' 'l' 'o'
```

C 样式转义字符 (如\\0 或\\n) 不能使用以下命令。

如果省略*值*参数，系统将提示你输入。 将显示的地址，其当前内容，并**输入&gt;** 提示符将显示。 然后，您可以执行以下任一操作：

-   输入新值，通过键入值并按 ENTER。

-   通过按 ENTER 后跟的空间保留在内存中的当前值。

-   通过按 ENTER 退出命令。

 

 





