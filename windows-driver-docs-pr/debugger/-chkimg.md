---
title: chkimg
description: Chkimg 扩展的可执行文件的图像中检测到通过与符号存储区或其他文件存储库上的副本进行比较的损坏。
ms.assetid: 8079676c-1138-4c60-95df-62fd270fee62
keywords:
- 可执行文件和路径，损坏
- chkimg Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chkimg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae67307c931ac6a412275351e5366107daa5ea36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336906"
---
# <a name="chkimg"></a>!chkimg


**！ Chkimg**扩展检测损坏的可执行文件的映像中将它们与符号存储区或其他文件存储库上的副本进行比较。

```dbgsyntax
!chkimg [Options] [-mmw LogFile LogOptions] [Module]
```

## <a name="span-idddkchkimgdbgspanspan-idddkchkimgdbgspanparameters"></a><span id="ddk__chkimg_dbg"></span><span id="DDK__CHKIMG_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项的任意组合：

<span id="-p_SearchPath_"></span><span id="-p_searchpath_"></span><span id="-P_SEARCHPATH_"></span>**-p** **** *SearchPath*   
以递归方式搜索*SearchPath*之前访问符号服务器的文件。

<span id="-f"></span><span id="-F"></span>**-f**  
在图中修复错误。 每当扫描在内存中检测到符号存储区上的文件和映像之间的差异，符号存储区上的文件的内容复制图像上方。 如果您正在执行实时调试，在执行之前，可以创建转储文件 **！ chkimg f**扩展。

<span id="-nar"></span><span id="-NAR"></span>**-nar**  
防止符号服务器上的文件的映射的图像移动。 默认情况下，当位于符号服务器上文件的副本并将其映射到内存中， **！ chkimg**移动符号服务器上的文件的映像。 但是，如果您使用 **-nar**选项，从服务器文件的图像不会被移动。

已在内存 (正在扫描的 1) 的可执行文件映像被移动，因为调试器始终重新定位到它所加载的映像。

此开关是仅在操作系统已移动原始图像。 如果图像未移动， **！ chkimg** ，调试器会将该映像。 此开关的使用很少见。

<span id="-ss_SectionName_"></span><span id="-ss_sectionname_"></span><span id="-SS_SECTIONNAME_"></span>**-ss** **** *SectionName*   
限制到其名称中包含字符串这些部分扫描*SectionName*。 扫描将包含任何非可放弃部分名称中包含此字符串。 *SectionName*区分大小写，不能超过 8 个字符。

<span id="-as"></span><span id="-AS"></span>**-as**  
会导致扫描以包括除可放弃部分图像的所有部分。 默认情况下 (如果不使用 **-作为**或 **-ss**)，均可写的部分、 不是可执行文件的部分，其名称中包含"页"的部分和可放弃部分，将跳过扫描。

<span id="-r_StartAddress_EndAddress__"></span><span id="-r_startaddress_endaddress__"></span><span id="-R_STARTADDRESS_ENDADDRESS__"></span>**-r** **** *StartAddress* **** *EndAddress*   
限制到开头的内存范围扫描*StartAddress*结尾*EndAddress*。 在此范围内，通常会扫描任何部分进行扫描。 如果与此范围部分重叠部分，只有这一部分与此范围重叠的部分进行扫描。 扫描仅限于此范围内，即使还使用 **-作为**或 **-ss**切换。

<span id="-nospec"></span><span id="-NOSPEC"></span>**-nospec**  
会导致扫描以包括 Hal.dll 和 Ntoskrnl.exe 的保留的部分。 默认情况下 **！ chkimg**不会检查这些文件的某些部分。

<span id="-noplock"></span><span id="-NOPLOCK"></span>**-noplock**  
显示通过让 0x90 的字节值不匹配的区域 ( **nop**指令) 和 0xF0 的字节值 (**锁**指令)。 默认情况下，不显示这些不匹配。

<span id="-np"></span><span id="-NP"></span>**-np**  
原因修补说明能够识别。

<span id="-d"></span><span id="-D"></span>**-d**  
扫描正在进行中时显示的不匹配的所有区域的摘要。 有关此摘要文本的详细信息，请参阅备注部分。

<span id="-db"></span><span id="-DB"></span>**-db**  
将不匹配的区域显示的格式类似于[ **db 调试器命令**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)。 因此，每个显示行显示的第一个字节的地址在行中后, 跟最多 16 个十六进制字节值。 字节值后面的相应 ASCII 值。 所有非打印字符，如回车符和换行符，显示为句点 （.）。 由星号标记的不匹配的字节数 (\*)。

<span id="-lo_lines"></span><span id="-LO_LINES"></span>**-lo** **** *lines*  
限制输出的数目的线条 **-d**或 **-db**显示行的行数。

<span id="-v"></span><span id="-V"></span>**-v**  
显示详细的信息。

<span id="_______-mmw______"></span><span id="_______-MMW______"></span> **-mmw**   
创建一个日志文件，并记录的活动 **！ chkimg**此文件中。 日志文件的每一行表示单个不匹配。

<span id="_______LogFile______"></span><span id="_______logfile______"></span><span id="_______LOGFILE______"></span> *LogFile*   
指定日志文件的完整路径。 如果指定的相对路径，路径是相对于当前路径。

<span id="_______LogOptions______"></span><span id="_______logoptions______"></span><span id="_______LOGOPTIONS______"></span> *LogOptions*   
指定日志文件的内容。 *LogOptions*是包含不同字母的串联的字符串。 日志文件中的每一行包含多个由逗号分隔的列。 这些列包含以下选项字母字母在出现的顺序指定的项*LogOptions*字符串。 可以多次包含以下选项。 必须包含至少一个选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">日志选项</th>
<th align="left">日志文件中包含的信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>v</p></td>
<td align="left"><p>虚拟地址的不匹配</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>偏移量 （相对地址） 的模块中的不匹配</p></td>
</tr>
<tr class="odd">
<td align="left"><p>文件</p></td>
<td align="left"><p>不匹配的地址相对应的符号</p></td>
</tr>
<tr class="even">
<td align="left"><p>S</p></td>
<td align="left"><p>包含不匹配的节的名称</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>在不匹配位置应为正确值</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>在不匹配位置不正确值</p></td>
</tr>
</tbody>
</table>

 

*LogOptions*还可以包含的部分，或任何以下其他选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">日志选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>o</p></td>
<td align="left"><p>如果具有该名称的文件<em>日志文件</em>已存在，覆盖现有文件。 默认情况下，调试器将新的信息追加到任何现有文件的末尾。</p></td>
</tr>
<tr class="even">
<td align="left"><p>t<em>String</em></p></td>
<td align="left"><p>将额外列添加到日志文件。 在本专栏中每个条目包含<em>字符串</em>。 <strong>T</strong><em>字符串</em>选项非常有用，如果要将新的信息追加到现有日志文件，您必须将新记录与旧区分开来。 无法添加间距<strong>t</strong>并<em>字符串</em>。 如果您使用<strong>t</strong>我<em>字符串</em>选项，它必须是中的最后一个选项<em>LogOptions</em>，因为<em>字符串</em>采取以包含所有显示的字符之前的下一步的空间。</p></td>
</tr>
</tbody>
</table>

 

例如，如果*LogOptions*是**rSewo**，日志文件的每一行包含不匹配位置和在该位置的预期和实际值的相对地址和部分名称。 此选项还会导致覆盖任何以前的文件。 可以使用 **-mmw**交换机多次如果你想要创建具有不同的选项的多个日志文件。 可以在同一时间创建最多 10 个日志文件。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定要检查的模块。 *模块*可以是模块、 模块的起始地址或模块中包含的任何地址的名称。 如果省略*模块*，调试器使用包含当前指令指针的模块。

<span></span>  

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当你使用 **！ chkimg**，它将在符号存储区中驻留的文件复制到内存中的可执行文件的映像进行比较。

该文件的所有部分进行了都比较，但部分的可放弃、，均可写，不是可执行文件，其名称中具有"页"或从 INITKDBG 除外。 您可以更改此行为可以通过使用 **-ss**， **-作为**，或 **-r**开关。

**！ chkimg**显示图像和文件之间的任何不匹配，为图像错误，但存在以下例外：

-   不检查都已通过导入地址表 (IAT) 被占用的地址。

-   未选中 Hal.dll 和 Ntoskrnl.exe 中某些特定的地址，因为这些部分已加载时发生的某些更改。 若要检查这些地址，包括 **-nospec**选项。

-   如果存在在文件中，字节值 0x90 和值 0xF0 位于相应字节的映像 （或相反），这种情况下被视为匹配项。 通常情况下，符号服务器持有一个版本同时单处理器中存在的二进制文件和多处理器版本。 在基于 x86 的处理器上，**锁**指令为 0xF0，并且此指令对应于**nop** (0x90) 指令中的单处理器版本。 如果你想 **！ chkimg**若要显示此对为不匹配，请设置 **-noplock**选项。

**请注意**  如果你使用 **-f**选项以修复图像不匹配 **！ chkimg**修复它认为错误这些不匹配。 例如， **！ chkimg** 0x90 字节到 0xF0 字节时才会改变您包括 **-noplock**。

 

当包括 **-d**选项， **！ chkimg**扫描正在进行中时显示所有不匹配的区域的摘要。 两个行上显示每个不匹配。 第一行包括范围、 范围末尾、 范围、 符号名称和自上一个错误 （在括号内） 对应的范围和字节数开始的偏移量的大小开始。 第二行括在方括号中，并在映像中包括了期望的十六进制字节值、 冒号和实际接触过的十六进制字节值。 如果该范围的长度超过 8 个字节，冒号之前和之后的冒号会显示第一个 8 字节。 下面的示例演示这种情况。

```dbgcmd
be000015-be000016  2 bytes - win32k!VeryUsefulFunction+15 (0x8)
     [ 85 dd:95 23 ]
```

有时，驱动程序通过使用挂钩、 重定向或其他方法更改 Microsoft Windows 内核的一部分。 即使不再位于堆栈的驱动程序可能已更改内核的一部分。 可以使用 **！ chkimg**扩展作为文件比较工具来确定 Windows 内核 （或任何其他图像） 中的哪些部分要更改的驱动程序和完全如何部分都将进行更改。 这种比较完整转储文件是最有效。

此外可以使用 **！ chkimg**连同[ **！ 有关\_每个\_模块**](-for-each-module.md)扩展来检查每个已加载模块的映像。 下面的示例演示这种情况。

```dbgcmd
!for_each_module !chkimg @#ModuleName 
```

假设您会遇到的 bug 检查，例如，并开始使用[ **！ 分析**](-analyze.md)。

```dbgcmd
kd> !analyze 
....
BugCheck 1000008E, {c0000005, bf920e48, baf75b38, 0}
Probably caused by : memory_corruption
CHKIMG_EXTENSION: !chkimg !win32k
....
```

在此示例中， [ **！ 分析**](-analyze.md)输出表明该内存损坏已发生并包括 CHKIMG\_建议 Win32k.sys 可能已损坏的模块的扩展行。 （即使如果此行不存在，则可以考虑在位于堆栈顶部的模块中可能已损坏）。使用启动 **！ chkimg**而无需任何开关，如以下示例所示。

```dbgcmd
kd> !chkimg win32k
Number of different bytes for win32k: 31
```

下面的示例显示了为内存损坏。 使用 **！ chkimg-d**以显示所有 Win32k 模块错误。

```dbgcmd
kd> !chkimg win32k -d
    bf920e40-bf920e46  7 bytes - win32k!HFDBASIS32::vSteadyState+1f
        [ 78 08 d3 78 0c c2 04:00 00 00 00 00 01 00 ]
    bf920e48-bf920e5f  24 bytes - win32k!HFDBASIS32::vHalveStepSize (+0x08)
        [ 8b 51 0c 8b 41 08 56 8b:00 00 00 00 00 00 00 00 ]
Number of different bytes for win32k: 31
```

当你尝试反汇编列出的第二个部分的图像已损坏时，可能会发生以下输出。

```dbgcmd
kd> u  win32k!HFDBASIS32::vHalveStepSize
win32k!HFDBASIS32::vHalveStepSize:
bf920e48 0000             add     [eax],al
bf920e4a 0000             add     [eax],al
bf920e4c 0000             add     [eax],al
bf920e4e 0000             add     [eax],al
bf920e50 7808            js win32k!HFDBASIS32::vHalveStepSize+0x12 (bf920e5a)
bf920e52 d3780c           sar     dword ptr [eax+0xc],cl
bf920e55 c20400           ret     0x4
bf920e58 8b510c           mov     edx,[ecx+0xc]
```

然后，使用 **！ chkimg f**来修复内存损坏。

```dbgcmd
kd> !chkimg win32k -f
Warning: Any detected errors will be fixed to what we expect!
Number of different bytes for win32k: 31 (fixed)
```

现在可以反汇编更正后的视图，并查看所做的更改。

```dbgcmd
kd> u  win32k!HFDBASIS32::vHalveStepSize
win32k!HFDBASIS32::vHalveStepSize:
bf920e48 8b510c           mov     edx,[ecx+0xc]
bf920e4b 8b4108           mov     eax,[ecx+0x8]
bf920e4e 56               push    esi
bf920e4f 8b7104           mov     esi,[ecx+0x4]
bf920e52 03c2             add     eax,edx
bf920e54 c1f803           sar     eax,0x3
bf920e57 2bf0             sub     esi,eax
bf920e59 d1fe             sar     esi,1
```

 

 





