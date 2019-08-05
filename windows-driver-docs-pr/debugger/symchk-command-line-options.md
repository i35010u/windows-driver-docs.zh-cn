---
title: SymChk 命令行选项
description: SymChk 使用以下语法
ms.assetid: e17dd001-2830-49bd-b727-fcd772ee23b4
keywords:
- SymChk 命令行选项 Windows 调试
ms.date: 03/13/2019
topic_type:
- apiref
api_name:
- SymChk Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af4639590b1e434e15273f978c192112d78096c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379741"
---
# <a name="symchk-command-line-options"></a>SymChk 命令行选项


SymChk 使用以下语法：

```dbgcmd
symchk [/r] [/v | /q ] FileNames /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ie ExeFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /id DumpFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ih HotFixFile /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /ip ProcessID /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /it TextFileList /s[Opts] SymbolPath Options

symchk [/r] [/v | /q ] /om Manifest FileNames

symchk [/v | /q ] /im ManifestList /s[Opts] SymbolPath Options

symchk [/v | /q ] /om Manifest /ie ExeFile

symchk [/v | /q ] /om Manifest /id DumpFile

symchk [/v | /q ] /om Manifest /ih HotFixFile

symchk [/v | /q ] /om Manifest /ip ProcessFile

symchk [/v | /q ] /om Manifest /it TextFileList
```

## <a name="span-idddk_symchk_command_line_options_dtoolqspanspan-idddk_symchk_command_line_options_dtoolqspanparameters"></a><span id="ddk_symchk_command_line_options_dtoolq"></span><span id="DDK_SYMCHK_COMMAND_LINE_OPTIONS_DTOOLQ"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
如果*文件*指定的目录 **/r**选项将导致 SymChk 以递归方式搜索程序文件的此目录下的所有子目录。

<span id="________v______"></span><span id="________V______"></span> **/v**   
显示详细的信息。 这包括的符号已调查每个程序文件的文件名以及它是否传递、 失败或已被忽略。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
启用安静模式。 将取消所有输出 (除非 **/ot**已包含选项)。

<span id="_______FileNames______"></span><span id="_______filenames______"></span><span id="_______FILENAMES______"></span> *FileNames*   
指定的符号都要检查的程序文件。 允许使用绝对路径、 相对路径和 UNC 路径。 一个星号 ( **\\** <em>) 允许使用通配符。如果 * 文件名</em>以斜杠结尾，则会将其为目录名称，并检查该目录中的所有文件中。 如果*文件名*包含空格，则必须用引号引起来。

<span id="________ie_______ExeFile______"></span><span id="________ie_______exefile______"></span><span id="________IE_______EXEFILE______"></span> **/ie** *ExeFile*   
指定当前正在执行的程序的名称。 将检查此程序的符号。 *ExeFile*必须包含名称的文件和文件扩展名 (通常为.exe)，但没有路径信息。 如果有两个不同的可执行文件相同的名称，不建议此选项。 *ExeFile*可以指定任何其他程序，包括内核模式驱动程序。 如果*ExeFile*是一个星号 ( **\\** *)，SymChk 将检查所有正在运行的进程，包括驱动程序的符号。

<span id="________id_______DumpFile______"></span><span id="________id_______dumpfile______"></span><span id="________ID_______DUMPFILE______"></span> **/id** *DumpFile*   
指定的内存转储文件。 此转储文件的符号将进行检查。

<span id="________ih_______HotFixFile______"></span><span id="________ih_______hotfixfile______"></span><span id="________IH_______HOTFIXFILE______"></span> **/ih** *HotFixFile*   
指定一个自解压的修补程序 CAB 文件。

<span id="________ip_______ProcessID______"></span><span id="________ip_______processid______"></span><span id="________IP_______PROCESSID______"></span> **/ip** *ProcessID*   
指定当前正在执行的程序的进程 ID。 将检查此程序的符号。 *ProcessID*必须指定为十进制数。 有两个特殊通配符支持：

- 如果*ProcessID*为零 ( **0** )，SymChk 会检查正在运行的所有驱动程序的符号。

- 如果*ProcessID*是一个星号 ( **\\** *)，SymChk 将检查所有正在运行的进程，包括驱动程序的符号。

<span id="________it_______TextFileList______"></span><span id="________it_______textfilelist______"></span><span id="________IT_______TEXTFILELIST______"></span> **/it** *TextFileList*   
指定包含程序文件的列表的文本文件。 将检查所有这些程序的符号。 *TextFileList*必须指定一个文件 （通过相对、 绝对路径或 UNC 路径，但不带通配符）; 如果它包含它应括在引号中的空格。 在此文件中，每个行指示 （通过相对、 绝对路径或 UNC 路径），一个程序文件和一个星号通配符 (* *\\* * *) 允许。 但是，任何行，使用此通配符必须使用相对路径。

如果此文件中的行包含空格，应括在引号中。 此文件中的分号是注释字符--分号和行尾之间的所有内容都将被忽略。

<span id="________im_______ManifestList______"></span><span id="________im_______manifestlist______"></span><span id="________IM_______MANIFESTLIST______"></span> **/im** *ManifestList*   
指定命令的输入是通过使用以前创建的清单文件 **/om**参数。 清单文件包含有关为其检索符号文件的信息。 有关使用清单文件的详细信息，请参阅[清单文件中使用 SymChk](using-a-manifest-file-with-symchk.md)。

<span id="________om_______Manifest______"></span><span id="________om_______manifest______"></span><span id="________OM_______MANIFEST______"></span> **/om** *清单*   
指定创建清单文件。 清单文件包含有关一组符号将检索其，通过使用的文件的信息 **/im**参数，在更高版本时。

<span id="________s_Opts__SymbolPath"></span><span id="________s_opts__symbolpath"></span><span id="________S_OPTS__SYMBOLPATH"></span> **/s**\[*Opts*\] *SymbolPath*  
指定包含符号的目录。 允许使用绝对路径、 相对路径和 UNC 路径。 可以指定任意数目的目录--应使用分号分隔多个目录。 如果*SymbolPath*包含空格，则必须用引号引起来。 如果你想要指定此路径中的符号服务器，应使用以下语法之一：

```dbgcmd
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

不建议，则省略 **/s**\[*Opts* \] *SymbolPath*参数，但如果省略，SymChk 将指向公共通过使用以下默认路径的符号存储区：

```dbgcmd
srv*%SystemRoot%\symbols*https://msdl.microsoft.com/download/symbols
```

任意数量的以下选项可以按照 **/s**。 可以有之间没有空格 **/s**和这些选项：

<span id="e"></span><span id="E"></span>**e**  
SymChk 将检查每个路径，而在一次检查所有路径不是单独。

<span id="u"></span><span id="U"></span>**u**  
将更新下游存储。 如果符号路径中包含的下游存储，在符号存储区将搜索符号文件。 将更新 SymChk 要检查的唯一符号存储区。

<span id="p"></span><span id="P"></span>**p**  
强制检查私有符号。 公共符号将被视为不匹配。 **P**选项暗指**e**并**u**，并不能用于**s**。

<span id="s"></span><span id="S"></span>**s**  
强制检查公共 （拆分） 符号。 私有符号将被视为不匹配。 **S**选项暗指**e**并**u**，并不能用于**p**。

<span id="r"></span><span id="R"></span>**r**  
为了进行深度搜索路径的展开指定的路径中的所有非符号服务器元素。 注意：此选项可能会产生不会在该调试器内因为它会修改指定的符号路径的匹配项。


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可用的选项划分为多个类。 每个类选项控制一组不同的功能。

**输出选项。** 可以指定任意数量的以下选项。 这些选项可以使用缩写 **/o**仅一次-例如， **/oi /oe**可以将其写作 **/oie**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/oe</strong></p></td>
<td align="left"><p>输出将包含各个错误。 此选项才有用如果<strong>/q</strong>使用，因为如果尚未激活安静模式下，将自动显示各个错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/op</strong></p></td>
<td align="left"><p>输出会列出传递每个文件。 （默认情况下，SymChk 仅显示失败测试的文件。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/oi</strong></p></td>
<td align="left"><p>输出会列出每个文件都被忽略。 （默认情况下，SymChk 仅显示失败测试的文件。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/od</strong></p></td>
<td align="left"><p>输出将包含完整详细信息。 与相同<strong>/oe /op /oi</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ot</strong></p></td>
<td align="left"><p>输出将包含结果总和。 此选项才有用如果<strong>/q</strong>使用，因为如果尚未激活安静模式下，将自动显示这些总计。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ob</strong></p></td>
<td align="left"><p>将所有输出消息中包括二进制文件的完整路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/os</strong></p></td>
<td align="left"><p>将所有输出消息中包括的符号的完整路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/oc</strong> <em>Dir</em></p></td>
<td align="left"><p>SymChk 将在目录中创建传统的符号树<em>Dir</em> ，其中包含一系列检查的所有符号文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ov</strong></p></td>
<td align="left"><p>SymChk 将打印也已检查二进制文件的版本信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ o l</strong> <em>文件</em></p></td>
<td align="left"><p>除了发送到标准输出的消息，写入文件，其中包含一个逗号分隔的所有二进制文件和传递符号检查其符号的列表。</p></td>
</tr>
</tbody>
</table>

 

**DBG 文件选项。** 这些选项可控制如何检查 SymChk *.dbg*符号文件。 可以指定仅以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ds</strong></p></td>
<td align="left"><p>SymChk 将验证.dbg 信息从可执行文件中去除，仅出现在.dbg 文件中，并可执行文件指向.dbg 文件。 如果程序没有.dbg 符号文件的情况下生成，则此选项无效。 这是默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/de</strong></p></td>
<td align="left"><p>SymChk 将验证.dbg 信息已不去除从可执行文件和可执行文件不指向.dbg 文件。 如果程序没有.dbg 符号文件的情况下生成，则此选项无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/dn</strong></p></td>
<td align="left"><p>不在图中，存在.dbg 信息和图像不指向.dbg 文件，将验证 SymChk。</p></td>
</tr>
</tbody>
</table>

 

**PDB 文件选项。** 这些选项控制 SymChk 检查.pdb 符号文件的方式。 可以指定仅以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/pf</strong></p></td>
<td align="left"><p>SymChk 不执行检查的.pdb 文件的内容--它只会验证这些文件存在并匹配二进制文件。 这是默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ps</strong></p></td>
<td align="left"><p>SymChk 将验证有已.pdb 文件抽取的源行、 数据类型和全局信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/pt</strong></p></td>
<td align="left"><p>SymChk 将验证，.pdb 文件中包含的数据类型信息。</p></td>
</tr>
</tbody>
</table>

 

**筛选选项。** 这些选项控制如何模块时未执行筛选 SymChk 正在检查的进程或转储文件。 可以指定仅以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/fm</strong> <em>Module</em></p></td>
<td align="left"><p>SymChk 仅会检查转储文件或与指定的模块关联的进程。 <em>模块</em>必须包含完整的文件名，但不能包含目录路径的任何部分。</p></td>
</tr>
</tbody>
</table>

 

**检查选项的符号。** 可以指定任意数量的以下选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/cs</strong></p></td>
<td align="left"><p>SymChk 不会验证 CodeView 数据存在。 （默认情况下存在的 CodeView 数据进行验证。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/cc</strong></p></td>
<td align="left"><p>当 SymChk 正在检查修补程序 CAB 文件时，则将不查找 cab 中的符号。 （默认情况下，SymChk 看起来如下所示提供的符号路径，也 cab 中的符号。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ea</strong> <em>文件</em></p></td>
<td align="left"><p>SymChk 不会验证指定的文件中列出的程序的符号。 这可以禁止某些程序，否则会进行验证。 <em>文件</em>必须指定一个文件 （通过相对、 绝对路径或 UNC 路径，但不带通配符）; 如果它包含它应括在引号中的空格。 内<em>文件</em>，每行表示程序文件 （通过相对、 绝对路径或 UNC 路径），允许使用任何通配符。 如果此文件中的行包含它应括在引号中的空格。 此文件中的分号是注释字符--分号和行尾之间的所有内容都将被忽略。 如果使用符号服务器，则这些程序的符号将不复制到下游的存储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ee</strong> <em>File</em></p></td>
<td align="left"><p>禁止在指定的文件中列出这些程序的错误消息。 "成功"和"忽略"消息将像往常一样，显示和符号文件将复制到下游存储像往常一样。 格式<em>文件</em>并且其内容的格式，对于相同<strong>/ea</strong> <em>文件</em>。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 SymChk 详细信息，请参阅[使用 SymChk](using-symchk.md)。

 

 





