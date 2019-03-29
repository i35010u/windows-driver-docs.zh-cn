---
title: s（搜索内存）
description: 通过内存以查找特定字节模式搜索 s 命令。
ms.assetid: fdca07c3-95c8-46cf-8da1-07a5e6767f67
keywords:
- s （内存搜索） Windows 调试
ms.date: 02/21/2019
topic_type:
- apiref
api_name:
- s (Search Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25e1a5b4f3e2c222b1822cd59452122ef1762f68
ms.sourcegitcommit: a43a696c5b4d2f08ee77d507631b41ecfdea6742
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56666731"
---
# <a name="s-search-memory"></a>s（搜索内存）


**S**命令通过内存以查找特定字节模式的搜索。

不要将使用此命令相混淆[ **~ s （更改当前处理器）**](-s--change-current-processor-.md)， [ **~ （设置当前线程） s**](-s--set-current-thread-.md)， [ **| s （集当前进程）**](-s--set-current-process-.md)，或[ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令。

```dbgcmd
s [-[[Flags]Type]] Range Pattern 
s -[[Flags]]v Range Object 
s -[[Flags]]sa Range 
s -[[Flags]]su Range 
```

## <a name="span-idddkcmdsearchmemorydbgspanspan-idddkcmdsearchmemorydbgspanparameters"></a><span id="ddk_cmd_search_memory_dbg"></span><span id="DDK_CMD_SEARCH_MEMORY_DBG"></span>参数


<span id="_______________Flags______________"></span><span id="_______________flags______________"></span><span id="_______________FLAGS______________"></span> **\[** *标志*\]   
指定一个或多个搜索选项。 每个标记都是单个字母。 必须将标志括在一组方括号 (\[\])。 不能之间除添加大括号之间空格**n**或**l**及其参数。 例如，如果你想要指定**s**并**w**选项，请使用的命令 s-\[sw\]类型范围模式。

您可以指定一个或多个下列标志：

<span id="s"></span><span id="S"></span>**s**  
将保存的所有当前的搜索结果中。 这些结果可用于更高版本重复搜索。

<span id="r"></span><span id="R"></span>**r**  
将当前的搜索结果限制从最后一个已保存的搜索。 不能使用**s**并**r**在同一命令中的标志。 当你使用**r**的值*范围*将被忽略，并且调试器将搜索由上一个保存这些命中数**s**命令。

<span id="n_Hits"></span><span id="n_hits"></span><span id="N_HITS"></span>**n** *命中数*  
指定保存时使用的命中次数**s**标志。 默认值为 1024年命中数。 如果您使用**n**与其他标志一起**n**必须是最后一个标志后, 跟其*命中*参数。 之间的间距**n**并*命中*是可选的但不能添加括号内的任何其他空间。 如果任何更高版本搜索，则使用**s**标志发现多个指定的命中数**溢出错误**显示消息来通知你并不是所有的命中数将被保存。

<span id="l_Length"></span><span id="l_length"></span><span id="L_LENGTH"></span>**l** *长度*  
为任意 ASCII 或 Unicode 字符串，以返回至少的字符串搜索将导致*长度*个字符。 默认长度为 3。 此值会影响使用的唯一搜索 **-sa**或**su**标志。

<span id="w"></span><span id="W"></span>**w**  
搜索只可写内存区域。 必须将"w"括在方括号中。

<span id="1"></span>**1**  
显示仅搜索的地址匹配搜索输出中的项。 如果你使用此选项很有用[ **.foreach** ](-foreach.md)令牌将命令输出传输到另一个命令的输入。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定要搜索的内存类型。 添加连字符 （-） 的前面*类型*。 可以使用下列任一*类型*值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>b</strong></p></td>
<td align="left"><p>字节 （8 位）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>w</strong></p></td>
<td align="left"><p>WORD （16 位）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>DWORD （32 位）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>q</strong></p></td>
<td align="left"><p>QWORD （64 位）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>a</strong></p></td>
<td align="left"><p></p>
ASCII 字符串 （不一定是以 null 终止字符串）</td>
</tr>
<tr class="even">
<td align="left"><p><strong>u</strong></p></td>
<td align="left"><p></p>
Unicode 字符串 （不一定是以 null 终止字符串）</td>
</tr>
</tbody>
</table>

 

如果省略*类型*，将使用字节值。 但是，如果您使用*标志*，不能省略*类型*。

<span id="_______sa______"></span><span id="_______SA______"></span> **sa**   
搜索包含可打印的 ASCII 字符串的任何内存。 使用**l** *长度*标志，用于指定此类字符串的最小长度。 默认最小长度为 3 个字符。

<span id="_______su______"></span><span id="_______SU______"></span> **su**   
搜索包含可打印的 Unicode 字符串的任何内存。 使用**l** *长度*标志，用于指定此类字符串的最小长度。 默认最小长度为 3 个字符。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定要搜索的内存区域。 除非您使用，此范围不能为 256MB 长**L？** 语法。 有关此语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定要搜索的一个或多个值。 默认情况下，这些值是字节值。 您可以指定不同类型的内存*类型*。 如果指定的单词、 双字节或 QWORD 值，具体取决于其他选择的选项，您可能需要将搜索模式括在单引号 (例如， **'H'**)。 

```dbgcmd
0:000> s -d @rsp L1000000 'H'  
0000003f`ff07ec00  00000048 00000000 500c0163 00000000  H.......c..P....
0000003f`ff07ec50  00000048 00000000 00000080 00000000  H...............
0000003f`ff07efc0  00000048 00000000 400c0060 00000000  H.......`..@....
```

如果指定的字符串，使用 ascii 类型中，将其括在双引号内 (例如， **"B7"**)。

```dbgcmd
0:000> s -a @rsp L10000000 "B7"  
0000003f`ff07ef0a  42 37 ff 7f 00 00 90 38-4e c2 6c 01 00 00 7d 26  B7.....8N.l...}&
0000003f`ff0ff322  42 37 ff 7f 00 00 f8 5d-42 37 ff 7f 00 00 20 41  B7.....]B7.... A
0000003f`ff0ff32a  42 37 ff 7f 00 00 20 41-42 37 ff 7f 00 00 98 59  B7.... AB7.....Y
```

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
搜索与指定的相同类型的对象*对象*。

<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定对象的地址或指向对象的指针的地址。 调试器则搜索与对象相同的类型的对象的*对象*指定。

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

有关内存操作和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果调试器在找到你指定的字节模式，调试器将显示中的第一个内存地址*范围*找到该模式的内存区域。 调试器将显示在匹配所指定的格式的该位置开始的内存的一段摘录*类型*内存类型。 如果*类型*是或**u**，显示内存内容和对应的 ASCII 或 Unicode 字符。

必须指定*模式*参数作为一系列字节，除非您指定不同*类型*值。 你可以输入字节值作为数值或 ASCII 字符：

-   数字值被解释为当前基数 （16、 10 或 8） 中的数字。 若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。
    **请注意**  默认基数以不同方式行为当你使用 c + + 表达式。 有关这些表达式和基数的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

     

-   必须用直单引号引起来将 ASCII 字符。 不能使用 C 样式的转义符 (如\\0 或\\n)。

如果指定多个字节时，必须用空格分隔它们。

**S a**并**s-u**命令搜索指定的 ASCII 和 Unicode 字符串，分别。 这些字符串不需要以 null 结尾。

**S sa**并**s su**命令未指定的 ASCII 和 Unicode 字符串进行搜索。 这些是内存的很有用，如果您要检查以查看它是否包含任何可打印字符范围。 标志选项，可以指定要查找字符串的最小长度。

例如：以下命令将查找 ASCII 字符串长度的&gt;= 3 开始 0000000140000000 和更高版本结束 400 字节的范围中。

```dbgcmd
s-sa 0000000140000000 L400
```

以下命令将查找 ASCII 字符串长度的&gt;= 开始 0000000140000000 和更高版本结束 400 字节的范围中的 4

```dbgcmd
s -[l4]sa 0000000140000000 L400
```

以下命令执行同样的操作，但它将搜索限定为可写内存区域。

```dbgcmd
s -[wl4]sa 0000000140000000 L400
```

下面的命令执行同样的操作，但显示仅的地址匹配，而不是地址以及值。

```dbgcmd
s -[1wl4]sa 0000000140000000 L400
```

**S-v**命令与相同的数据类型的对象的搜索*对象*对象。 仅当所需的对象是 c + + 类或具有虚函数表 (Vtable) 相关联的另一个对象，可以使用此命令。 **S-v**命令搜索*范围*内存区域中针对此类的 Vtable 的地址。 如果多个 Vtable 存在此类中，搜索算法将查找所有这些指针值，分隔适当数目的字节数。 如果找到任何匹配项，调试器将返回的对象和有关此对象-类似的输出的完整信息的基址[ **dt （显示类型）** ](dt--display-type-.md)命令。

例如：假定当前基数为 16。 以下三个命令全部执行相同的操作： 通过 0012FF5F 内存位置 0012FF40 搜索"Hello"。

```dbgcmd
0:000> s 0012ff40 L20 'H' 'e' 'l' 'l' 'o' 
```

```dbgcmd
0:000> s 0012ff40 L20 48 65 6c 6c 6f 
```

```dbgcmd
0:000> s -a 0012ff40 L20 "Hello" 
```

这些命令找到每个外观的"Hello"，并返回每个此类模式-即，字母"H"的地址的地址。

在调试器中的搜索范围返回完全包含的模式。 正确找到重叠模式。 （换句话说，模式"QQQ"中找到了三次"QQQQQ"。）

下面的示例演示使用的搜索*类型*参数。 此命令搜索通过 0012FF5F 双字 VUTS 为内存位置 0012FF40:

```dbgcmd
0:000> s -d 0012ff40 L20 'VUTS' 
```

小字节序在计算机上，VUTS' is 字节模式的相同 'T' 'U' V。 但是，搜索词，dword 值和 QWORDs 返回是正确的字节对齐的结果。

 

 





