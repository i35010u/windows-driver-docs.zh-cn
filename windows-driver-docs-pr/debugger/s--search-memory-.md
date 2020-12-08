---
title: s（搜索内存）
description: S 命令在内存中搜索以查找特定的字节模式。
keywords:
- s (搜索内存) Windows 调试
ms.date: 02/21/2019
topic_type:
- apiref
api_name:
- s (Search Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d32d6d9a912af99249b7df81a45e1f0614f919a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830245"
---
# <a name="s-search-memory"></a>s（搜索内存）


**S** 命令在内存中搜索以查找特定的字节模式。

请勿将此命令与 [**~ s (更改当前处理器)**](-s--change-current-processor-.md)， [**~ s (设置当前线程)**](-s--set-current-thread-.md)， [**| s (设置当前进程)**](-s--set-current-process-.md)或 [**| |s (设置当前系统)**](--s--set-current-system-.md) 命令。

```dbgcmd
s [-[[Flags]Type]] Range Pattern 
s -[[Flags]]v Range Object 
s -[[Flags]]sa Range 
s -[[Flags]]su Range 
```

## <a name="span-idddk_cmd_search_memory_dbgspanspan-idddk_cmd_search_memory_dbgspanparameters"></a><span id="ddk_cmd_search_memory_dbg"></span><span id="DDK_CMD_SEARCH_MEMORY_DBG"></span>参数


<span id="_______________Flags______________"></span><span id="_______________flags______________"></span><span id="_______________FLAGS______________"></span>**\[***标志*\]   
指定一个或多个搜索选项。 每个标志均为一个字母。 必须将标志括在一组方括号中， (\[ \]) 。 不能在方括号之间添加空格，除非在 **n** 或 **l** 与参数之间。 例如，如果想要指定 **s** 和 **w** 选项，请使用命令 s- \[ sw \] 类型范围模式。

可以指定以下一个或多个标志：

<span id="s"></span><span id="S"></span>**些**  
保存当前搜索的所有结果。 您可以使用这些结果来稍后重复搜索。

<span id="r"></span><span id="R"></span>**迅驰**  
将当前搜索限制为上次保存的搜索结果。 不能在同一命令中使用 **s** 和 **r** 标志。 使用 **r** 时，将忽略 *范围* 的值，并且调试器只搜索前面的 **s** 命令保存的命中。

<span id="n_Hits"></span><span id="n_hits"></span><span id="N_HITS"></span>**n** 次 *命中*  
指定使用 **s** 标志时要保存的命中数。 默认值为1024。 如果将 **n** 与其他标志一起使用，则 **n** 必须是最后一个标志，后跟其 *命中* 参数。 **N** 和 *命中* 之间的空格是可选的，但不能在括号内添加任何其他空格。 如果以后 **使用标志的** 搜索发现超过指定的命中次数，则会显示 **溢出错误** 消息，通知您并未保存所有命中。

<span id="l_Length"></span><span id="l_length"></span><span id="L_LENGTH"></span>**l** *Length*  
导致搜索任意 ASCII 或 Unicode 字符串，以便仅返回 *长度* 至少为个字符的字符串。 默认长度为3。 此值仅影响使用 **-sa** 或 **-su** 标志的搜索。

<span id="w"></span><span id="W"></span>**水平**  
仅搜索可写内存区域。 必须将 "w" 括在括号中。

<span id="1"></span>**1**  
只显示搜索输出中搜索匹配项的地址。 如果使用 [**foreach**](-foreach.md) 标记通过管道将命令输出传递给另一个命令输入，则此选项很有用。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定要搜索的内存类型。 在 *类型* 前面添加连字符 ( ) 。 您可以使用以下 *类型* 的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">类型</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>b</strong></p></td>
<td align="left"><p>字节 (8 位) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>w</strong></p></td>
<td align="left"><p>WORD (16 位) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>DWORD (32 位) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>：</strong></p></td>
<td align="left"><p>QWORD (64 位) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>的</strong></p></td>
<td align="left"><p></p>
ASCII 字符串 (不一定是以 null 结尾的字符串) </td>
</tr>
<tr class="even">
<td align="left"><p><strong>u</strong></p></td>
<td align="left"><p></p>
Unicode 字符串 (不一定是以 null 结尾的字符串) </td>
</tr>
</tbody>
</table>

 

如果省略 *类型*，则使用字节值。 但是，如果使用 *标志*，则不能省略 *类型*。

<span id="_______sa______"></span><span id="_______SA______"></span>**sa**   
搜索包含可打印的 ASCII 字符串的任何内存。 使用 **l** *长度* 标志来指定此类字符串的最小长度。 默认的最小长度为3个字符。

<span id="_______su______"></span><span id="_______SU______"></span>**su**   
搜索包含可打印的 Unicode 字符串的任何内存。 使用 **l** *长度* 标志来指定此类字符串的最小长度。 默认的最小长度为3个字符。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要在其中进行搜索的内存区域。 除非使用 **L？** 语法，否则此范围不能超过 256 MB。 有关此语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定要搜索的一个或多个值。 默认情况下，这些值是字节值。 你可以在 *类型* 中指定不同类型的内存。 如果根据选择的其他选项指定字、DWORD 或 QWORD 值，可能需要将搜索模式括在单引号中 (例如， **"H"**) 。 

```dbgcmd
0:000> s -d @rsp L1000000 'H'  
0000003f`ff07ec00  00000048 00000000 500c0163 00000000  H.......c..P....
0000003f`ff07ec50  00000048 00000000 00000080 00000000  H...............
0000003f`ff07efc0  00000048 00000000 400c0060 00000000  H.......`..@....
```

如果使用 ascii 类型指定字符串，请用双引号将其引起来 (例如， **"B7"**) 。

```dbgcmd
0:000> s -a @rsp L10000000 "B7"  
0000003f`ff07ef0a  42 37 ff 7f 00 00 90 38-4e c2 6c 01 00 00 7d 26  B7.....8N.l...}&
0000003f`ff0ff322  42 37 ff 7f 00 00 f8 5d-42 37 ff 7f 00 00 20 41  B7.....]B7.... A
0000003f`ff0ff32a  42 37 ff 7f 00 00 20 41-42 37 ff 7f 00 00 98 59  B7.... AB7.....Y
```

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
搜索与指定 *对象* 具有相同类型的对象。

<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定对象的地址或指向对象的指针的地址。 然后，调试器会搜索与该 *对象* 指定的对象具有相同类型的对象。

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

有关内存操作的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果调试器找到你指定的字节模式，则调试器将在找到该模式的 *范围* 内存区域中显示第一个内存地址。 调试器将显示以与指定的 *类型* 内存类型匹配的格式从该位置开始的内存摘录。 如果 *类型* 为或 **u** **，则显示** 内存内容和对应的 ASCII 或 Unicode 字符。

除非指定不同的 *类型* 值，否则必须将 *模式* 参数指定为一系列字节。 可以输入字节值作为数字或 ASCII 字符：

-   数字值被解释为当前基数 (16、10或 8) 中的数字。 若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。 您可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来覆盖默认基数。
    **注意**   使用 c + + 表达式时，默认基数的行为不同。 有关这些表达式和基数的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

     

-   必须用单引号将 ASCII 字符括起来。 不能使用 C 样式转义符 (如 " \\ 0" 或 " \\ n" ) 。

如果指定多个字节，则必须用空格分隔它们。

**S a** 和 **s-u** 命令分别搜索指定的 ASCII 和 Unicode 字符串。 这些字符串不必以 null 结尾。

**S-sa** 和 **s-su** 命令搜索未指定的 ASCII 和 Unicode 字符串。 如果检查内存范围以查看它是否包含任何可打印字符，则这些方法很有用。 使用 "标志" 选项，可以指定要查找的字符串的最小长度。

示例：下面的命令从0000000140000000开始查找长度为 = 3 的 ASCII 字符串 &gt; ，稍后再结束400字节。

```dbgcmd
s-sa 0000000140000000 L400
```

以下命令在从0000000140000000开始的范围内查找长度为4的 ASCII 字符串 &gt; ，稍后再结束400字节

```dbgcmd
s -[l4]sa 0000000140000000 L400
```

下面的命令执行相同的操作，但它会将搜索限制为可写内存区域。

```dbgcmd
s -[wl4]sa 0000000140000000 L400
```

下面的命令执行相同的操作，但只显示匹配项的地址，而不显示地址和值。

```dbgcmd
s -[1wl4]sa 0000000140000000 L400
```

**S v** 命令搜索与 *对象* 对象具有相同数据类型的对象。 仅当所需的对象是一个 c + + 类或与 (Vtables) 的虚拟函数表关联的其他对象时，才能使用此命令。 对于此类的 Vtables 的地址， **s-v** 命令搜索 *范围* 内存区域。 如果此类中存在多个 Vtables，搜索算法将查找所有这些指针值，并以适当的字节数分隔。 如果找到任何匹配项，则调试器将返回对象的基址和与此对象有关的完整信息，类似于 [**dt (显示类型)**](dt--display-type-.md) 命令的输出。

示例：假定当前基数为16。 以下三个命令都执行相同的操作：搜索内存位置0012FF40 到 0012FF5F for "Hello"。

```dbgcmd
0:000> s 0012ff40 L20 'H' 'e' 'l' 'l' 'o' 
```

```dbgcmd
0:000> s 0012ff40 L20 48 65 6c 6c 6f 
```

```dbgcmd
0:000> s -a 0012ff40 L20 "Hello" 
```

这些命令将查找 "Hello" 的每个外观，并返回每个此类模式的地址，即字母 "H" 的地址。

调试器只返回完全包含在搜索范围中的模式。 正确找到了重叠模式。  (换言之，在 "QQQQQ" 中找到了 "QQQ" 模式三次。 ) 

下面的示例演示使用 *类型* 参数的搜索。 此命令搜索0012FF40 通过0012FF5F 的双字 "VUTS" 的内存位置：

```dbgcmd
0:000> s -d 0012ff40 L20 'VUTS' 
```

在小 endian 计算机上，"VUTS" 与字节模式的 "t" "U" "V" 相同。 不过，搜索词、Dword 和 QWORDs 只返回正确字节对齐的结果。

 

 





