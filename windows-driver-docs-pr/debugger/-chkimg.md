---
title: chkimg
description: Chkimg 扩展可通过将可执行文件的图像与符号存储或其他文件存储库上的副本进行比较来检测这些文件中的损坏。
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
ms.openlocfilehash: 542f79165a1eecfd878dd362691bae1f9f280034
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795769"
---
# <a name="chkimg"></a>!chkimg


**！ Chkimg** extension 通过将可执行文件的映像与符号存储或其他文件存储库上的副本进行比较，来检测这些文件中的损坏。

```dbgsyntax
!chkimg [Options] [-mmw LogFile LogOptions] [Module]
```

## <a name="span-idddk__chkimg_dbgspanspan-idddk__chkimg_dbgspanparameters"></a><span id="ddk__chkimg_dbg"></span><span id="DDK__CHKIMG_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
下列选项的任意组合：

<span id="-p_SearchPath_"></span><span id="-p_searchpath_"></span><span id="-P_SEARCHPATH_"></span>**-p**  **** *SearchPath*   
在访问符号服务器之前以递归方式搜索该文件的 *SearchPath* 。

<span id="-f"></span><span id="-F"></span>**-f**  
修复映像中的错误。 每当扫描检测到符号存储区中的文件和内存中的图像之间的差异时，会通过图像复制符号存储区上文件的内容。 如果要执行实时调试，可以在执行 **！ chkimg-f** 扩展之前创建转储文件。

<span id="-nar"></span><span id="-NAR"></span>**-nar**  
禁止移动符号服务器上的文件的映射图像。 默认情况下，当该文件的副本位于符号服务器上并映射到内存中时， **！ chkimg** 会将该文件的图像移到符号服务器上。 但是，如果使用 **-nar** 选项，则不会移动服务器中的文件图像。

已在内存中的可执行映像 (也就是说，要扫描) 的可执行映像会移动，因为调试器始终重新定位它加载的图像。

此开关仅在操作系统已移动原始映像时才有用。 如果尚未移动图像， **！ chkimg** 和调试器将移动图像。 很少使用此开关。

<span id="-ss_SectionName_"></span><span id="-ss_sectionname_"></span><span id="-SS_SECTIONNAME_"></span>**-ss**  **** *SectionName*   
将扫描限制为名称包含字符串 *SectionName* 的那些部分。 扫描将包含名称中包含此字符串的任何非可放弃部分。 *SectionName* 区分大小写，不能超过8个字符。

<span id="-as"></span><span id="-AS"></span>**-as**  
导致扫描包含图像的所有部分（可放弃部分除外）。 默认情况 (下，如果不使用 **-as** 或 **-ss**) ，扫描将跳过可写的节、不可执行的节、其名称中包含 "PAGE" 的节和可放弃节。

<span id="-r_StartAddress_EndAddress__"></span><span id="-r_startaddress_endaddress__"></span><span id="-R_STARTADDRESS_ENDADDRESS__"></span>**-r**  **** *StartAddress*  **** *EndAddress*   
将扫描限制为以 *StartAddress* 开头的内存范围，并以 *EndAddress* 结束。 在此范围内，将扫描通常会扫描的任何部分。 如果某个部分与此范围部分重叠，则只扫描部分与此范围重叠的部分。 即使你还使用 **-as** 或 **-ss** 交换机，扫描也仅限于此范围。

<span id="-nospec"></span><span id="-NOSPEC"></span>**-nospec**  
导致扫描包含 Hal.dll 和 Ntoskrnl.exe 的保留部分。 默认情况下， **！ chkimg** 不检查这些文件的某些部分。

<span id="-noplock"></span><span id="-NOPLOCK"></span>**-noplock**  
通过将一个字节值 0x90 (**nop**) 指令来显示不匹配的区域，并将0xF0 的字节值 (**锁定**) 指令。 默认情况下，不会显示这些不匹配。

<span id="-np"></span><span id="-NP"></span>**-np**  
导致识别修补的指令。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
在扫描发生时显示所有不匹配的区域的摘要。 有关此摘要文本的详细信息，请参阅 "备注" 部分。

<span id="-db"></span><span id="-DB"></span>**-db**  
以类似于 [**db 调试器命令**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)的格式显示不匹配的区域。 因此，每个显示行都显示行中第一个字节的地址，后跟多达16个十六进制字节值。 字节值后跟对应的 ASCII 值。 所有非打印字符（如回车符和换行符）都作为句点 ( 显示。 ) 。 不匹配的字节通过星号标记 (\*) 。

<span id="-lo_lines"></span><span id="-LO_LINES"></span>**-lo**  **** *行*  
将 **-d** 或 **-db** 显示的输出行的数目限制为行数。

<span id="-v"></span><span id="-V"></span>**-v**  
显示详细信息。

<span id="_______-mmw______"></span><span id="_______-MMW______"></span>**-mmw**   
创建一个日志文件，并在此文件中记录 **！ chkimg** 的活动。 日志文件的每一行都表示一个不匹配。

<span id="_______LogFile______"></span><span id="_______logfile______"></span><span id="_______LOGFILE______"></span>*日志文件*   
指定日志文件的完整路径。 如果指定相对路径，则该路径是相对于当前路径的路径。

<span id="_______LogOptions______"></span><span id="_______logoptions______"></span><span id="_______LOGOPTIONS______"></span>*LogOptions*   
指定日志文件的内容。 *LogOptions* 是一个字符串，其中包含各种字母的串联。 日志文件中的每一行都包含用逗号分隔的多个列。 这些列包含以下选项，这些项以字母在 *LogOptions* 字符串中出现的顺序指定。 可以多次包含以下选项。 必须至少包含一个选项。

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
<td align="left"><p>不匹配的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>模块内不匹配 (相对地址) 偏移量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>s</p></td>
<td align="left"><p>与不匹配的地址相对应的符号</p></td>
</tr>
<tr class="even">
<td align="left"><p>S</p></td>
<td align="left"><p>包含不匹配的节的名称</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>不匹配位置应为正确的值</p></td>
</tr>
<tr class="even">
<td align="left"><p>w</p></td>
<td align="left"><p>不匹配位置的错误值</p></td>
</tr>
</tbody>
</table>

 

*LogOptions* 还可以包含以下附加选项的部分或全部。

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
<td align="left"><p>如果 <em>已存在同名的</em> 文件，则将覆盖现有文件。 默认情况下，调试器会将新信息追加到任何现有文件的末尾。</p></td>
</tr>
<tr class="even">
<td align="left"><p>t<em>字符串</em></p></td>
<td align="left"><p>向日志文件添加额外的列。 此列中的每个条目都包含 <em>String</em>。 如果要将新信息追加到现有日志文件，并且必须将新记录与旧记录区分开来，则可以使用 <strong>t</strong><em>字符串</em> 选项。 不能在 <strong>t</strong> 和 <em>String</em>之间添加空格。 如果使用 <strong>t</strong>I<em>字符串</em> 选项，则它必须是 <em>LogOptions</em>中的最后一个选项，因为 <em>字符串</em> 将被视为包含在下一个空格之前的所有字符。</p></td>
</tr>
</tbody>
</table>

 

例如，如果 *LogOptions* 为 **rSewo**，则日志文件的每一行都包含不匹配位置的相对地址和节名称，以及该位置的预期值和实际值。 此选项还会导致覆盖以前的任何文件。 如果要创建具有不同选项的多个日志文件，可以多次使用 **-mmw** 开关。 你最多可以创建10个日志文件。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定要检查的模块。 *Module* 可以是模块名称、模块的起始地址或模块中包含的任何地址。 如果省略 *module*，则调试器将使用包含当前指令指针的模块。

<span></span>  

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

使用 **！ chkimg** 时，它会将内存中的可执行文件的图像与位于符号存储区中的文件的副本进行比较。

将比较文件的所有部分，但不包括可放弃的部分、可执行文件、名称中有 "PAGE" 或来自 INITKDBG 的部分除外。 可以通过使用 **-ss**、 **-as** 或 **-r** 开关来更改此行为。

**！ chkimg** 将图像和文件之间的任何不匹配显示为图像错误，但以下情况例外：

-   不检查导入地址表 (IAT) 占用的地址。

-   不会检查 Hal.dll 和 Ntoskrnl.exe 中的特定地址，因为加载这些节时会发生某些更改。 若要检查这些地址，请包含 **-nospec** 选项。

-   如果该文件中存在 byte 值0x90，并且) 值在该图像的相应 (中存在，则此情况被视为匹配。 通常，符号服务器包含在单处理器版本和多处理器版本中都存在的二进制文件的一个版本。 在基于 x86 的处理器上， **lock** 指令为0xF0，此指令对应于 **nop** (0x90) 单处理器版本中的指令。 如果希望 **！ chkimg** 显示此对不匹配，请设置 **-noplock** 选项。

**注意**   如果使用 **-f** 选项修复图像不匹配，则 **！ chkimg** 仅修复其视为错误的那些不匹配项。 例如， **！ chkimg** 不会将0x90 字节更改为0xF0 字节，除非包含 **-noplock**。

 

如果包括 **-d** 选项， **！ chkimg** 会在扫描发生时显示所有不匹配的区域的摘要。 每个不匹配项将显示在两行中。 第一行包括范围的开始位置、范围结束、范围的大小、与范围起始值相对应的符号名称和偏移量，以及自上次错误之后的字节数)  (。 第二行括在括号中，其中包括所需的十六进制字节值、冒号，然后是在图像中实际遇到的十六进制字节值。 如果该范围超过8个字节，则在冒号之前和冒号之后只显示前8个字节。 下面的示例演示了这种情况。

```dbgcmd
be000015-be000016  2 bytes - win32k!VeryUsefulFunction+15 (0x8)
     [ 85 dd:95 23 ]
```

有时，驱动程序使用挂钩、重定向或其他方法来更改 Microsoft Windows 内核的一部分。 即使不在堆栈上的驱动程序，也可能会改变内核部分。 您可以使用 **！ chkimg** extension 作为文件比较工具来确定 Windows 内核 (或任何其他映像) 正在由驱动程序更改的部分，以及确切地改变部件的方式。 此比较最有效地用于完整转储文件。

[**对于 \_ 每个 \_ 模块**](-for-each-module.md)扩展，还可以将 **！ chkimg** 与！一起用于检查每个已加载模块的映像。 下面的示例演示了这种情况。

```dbgcmd
!for_each_module !chkimg @#ModuleName 
```

假设您遇到了错误检查，例如，使用 [**！分析**](-analyze.md)开始。

```dbgcmd
kd> !analyze 
....
BugCheck 1000008E, {c0000005, bf920e48, baf75b38, 0}
Probably caused by : memory_corruption
CHKIMG_EXTENSION: !chkimg !win32k
....
```

在此示例中，" [**！分析**](-analyze.md) " 输出表明内存损坏已发生，并包含一个 CHKIMG \_ 延长线，这表明 Win32k.sys 可能是已损坏的模块。 即使此行不存在，也可能会考虑堆栈顶部的模块可能已损坏。 ) 从 chkimg 中使用 **！** 开始，如以下示例中所示。 (

```dbgcmd
kd> !chkimg win32k
Number of different bytes for win32k: 31
```

下面的示例说明确实存在内存损坏。 使用 **！ chkimg** 显示 win32k.sys 模块的所有错误。

```dbgcmd
kd> !chkimg win32k -d
    bf920e40-bf920e46  7 bytes - win32k!HFDBASIS32::vSteadyState+1f
        [ 78 08 d3 78 0c c2 04:00 00 00 00 00 01 00 ]
    bf920e48-bf920e5f  24 bytes - win32k!HFDBASIS32::vHalveStepSize (+0x08)
        [ 8b 51 0c 8b 41 08 56 8b:00 00 00 00 00 00 00 00 ]
Number of different bytes for win32k: 31
```

当你尝试拆装列出的第二个部分的损坏映像时，可能会出现以下输出。

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

然后，使用 **！ chkimg-f** 修复内存损坏。

```dbgcmd
kd> !chkimg win32k -f
Warning: Any detected errors will be fixed to what we expect!
Number of different bytes for win32k: 31 (fixed)
```

现在，你可以反汇编已更正的视图，并查看你所做的更改。

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

 

 





