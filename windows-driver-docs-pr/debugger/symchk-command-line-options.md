---
title: SymChk 命令行选项
description: SymChk 使用以下语法
keywords:
- SymChk Command-Line 选项 Windows 调试
ms.date: 03/13/2019
topic_type:
- apiref
api_name:
- SymChk Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e657002055cab9cfd19dd09305501b0efa562d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803985"
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


<span id="________r______"></span><span id="________R______"></span>**/r**   
如果 *文件* 指定一个目录，则 **/r** 选项会使 SymChk 以递归方式搜索此目录下的程序文件的所有子目录。

<span id="________v______"></span><span id="________V______"></span>**/v**   
显示详细信息。 这包括其符号已被检查的每个程序文件的文件名，以及是否已通过、失败或已被忽略。

<span id="________q______"></span><span id="________Q______"></span>**/q**   
启用安静模式。 除非) 包含 **/ot** 选项，否则所有输出都将被取消 (。

<span id="_______FileNames______"></span><span id="_______filenames______"></span><span id="_______FILENAMES______"></span>*文件名*   
指定要检查其符号的程序文件。 允许使用绝对路径、相对路径和 UNC 路径。 允许使用星号 ( * *\** _) 通配符。 如果 _FileNames 以 </em> 斜杠结束，则将其视为目录名称，并检查该目录中的所有文件。 如果 *文件名* 包含空格，则必须用引号将其引起来。

<span id="________ie_______ExeFile______"></span><span id="________ie_______exefile______"></span><span id="________IE_______EXEFILE______"></span>**/Ie** *ExeFile*   
指定当前正在执行的程序的名称。 将检查此程序的符号。 *ExeFile* 必须包含文件和文件扩展名的名称， (通常是 .exe) ，但不包含路径信息。 如果有两个具有相同名称的不同可执行文件，则不建议使用此选项。 *ExeFile* 可以指定任何程序，包括内核模式驱动程序。 如果 *ExeFile* 是 ( * _) 的单个星号 *\** ，则 SymChk 将检查所有正在运行的进程（包括驱动程序）的符号。

<span id="________id_______DumpFile______"></span><span id="________id_______dumpfile______"></span><span id="________ID_______DUMPFILE______"></span>_ */id* *  *DumpFile*   
指定内存转储文件。 将检查此转储文件的符号。

<span id="________ih_______HotFixFile______"></span><span id="________ih_______hotfixfile______"></span><span id="________IH_______HOTFIXFILE______"></span>**/Ih** *HotFixFile*   
指定一个自解压缩修补程序 CAB 文件。

<span id="________ip_______ProcessID______"></span><span id="________ip_______processid______"></span><span id="________IP_______PROCESSID______"></span>**/Ip** *ProcessID*   
指定当前正在执行的程序的进程 ID。 将检查此程序的符号。 *ProcessID* 必须指定为十进制数字。 支持两个特殊通配符：

- 如果 *ProcessID* 为零 ( **0** ) ，SymChk 将检查所有正在运行的驱动程序的符号。

- 如果 *ProcessID* 是 ( * _) 的单个星号 *\** ，SymChk 将检查所有正在运行的进程（包括驱动程序）的符号。

<span id="________it_______TextFileList______"></span><span id="________it_______textfilelist______"></span><span id="________IT_______TEXTFILELIST______"></span>_*/it* *  *TextFileList* 指定包含程序文件列表的文本文件。将检查所有这些程序的符号。*TextFileList* 必须仅指定一个文件 (按相对路径、绝对路径或 UNC 路径，但不) 通配符;如果包含空格，则应该用引号将其引起来。在此文件中，每一行都表示一个程序文件 (按相对路径、绝对路径或 UNC 路径) ，并允许 ( *\** *) 星号通配符_。 但是，使用此通配符的任何行都必须使用相对路径。

如果此文件中的行包含空格，则应将其括在引号中。 此文件中的分号是注释字符，在分号与行尾之间的所有内容都将被忽略。

<span id="________im_______ManifestList______"></span><span id="________im_______manifestlist______"></span><span id="________IM_______MANIFESTLIST______"></span>_ */im* *  *ManifestList*   
指定命令的输入是先前使用 **/om** 参数创建的清单文件。 清单文件包含要为其检索符号的文件的相关信息。 有关使用清单文件的详细信息，请参阅 [将清单文件与 SymChk 一起使用](using-a-manifest-file-with-symchk.md)。

<span id="________om_______Manifest______"></span><span id="________om_______manifest______"></span><span id="________OM_______MANIFEST______"></span>**/Om** *清单*   
指定创建清单文件。 清单文件包含有关一组文件的信息，这些文件将在以后使用 **/im** 参数进行检索。

<span id="________s_Opts__SymbolPath"></span><span id="________s_opts__symbolpath"></span><span id="________S_OPTS__SYMBOLPATH"></span>**/s** \[*Opts* " \]*SymbolPath*  
指定包含符号的目录。 允许使用绝对路径、相对路径和 UNC 路径。 可以指定任意数量的目录--应用分号分隔多个目录。 如果 *SymbolPath* 包含空格，则必须用引号将其引起来。 如果希望在此路径中指定符号服务器，则应使用以下语法之一：

```dbgcmd
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

不建议省略 **/s** \[ *Opts* \] *SymbolPath* 参数，但如果省略该参数，则 SymChk 将使用以下默认路径指向公共符号存储区：

```dbgcmd
srv*%SystemRoot%\symbols*https://msdl.microsoft.com/download/symbols
```

以下任意数量的选项都可以遵循 **/s**。 **/S** 和以下选项之间不能有空格：

<span id="e"></span><span id="E"></span>**电邮**  
SymChk 将单独检查每个路径，而不是一次检查所有路径。

<span id="u"></span><span id="U"></span>**形**  
下游存储将更新。 如果符号路径包含下游存储，将搜索符号存储区中的符号文件。 仅将更新 SymChk 检查的符号存储区。

<span id="p"></span><span id="P"></span>**h-p**  
强制检查私有符号。 公共符号将被视为不匹配。 **P** 选项隐含 **e** 和 **u**，不能 **与一起使用。**

<span id="s"></span><span id="S"></span>**些**  
强制检查公共 (拆分) 符号。 私有符号将被视为不匹配。 **S** 选项隐含 **e** 和 **u**，不能与 **p** 一起使用。

<span id="r"></span><span id="R"></span>**迅驰**  
展开指定路径中的所有非符号服务器元素，以便对路径进行深层搜索。 注意：此选项可能生成不会在调试器内发生的匹配项，因为它会修改指定的符号路径。


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可用选项分为多个类。 每类选项都控制一组不同的功能。

**输出选项。** 可以指定下列任意数量的选项。 可以使用 **/o** 只使用一次来缩写这些选项，例如，可以将 **/oi/oe** 编写为 **/oie**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/oe</strong></p></td>
<td align="left"><p>输出将包含单独的错误。 仅当使用 <strong>/q</strong> 时，此选项才有用，因为如果没有激活安静模式，将自动显示单个错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/op</strong></p></td>
<td align="left"><p>输出会列出传递的每个文件。  (默认情况下，SymChk 仅显示测试失败的文件。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/oi</strong></p></td>
<td align="left"><p>输出将列出已忽略的每个文件。  (默认情况下，SymChk 仅显示测试失败的文件。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/od</strong></p></td>
<td align="left"><p>输出将包括完整的详细信息。 与 <strong>/oe/op/oi</strong>相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ot</strong></p></td>
<td align="left"><p>输出将包含结果总计。 仅当使用 <strong>/q</strong> 时，此选项才有用，因为如果没有激活安静模式，则会自动显示这些总计。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ob</strong></p></td>
<td align="left"><p>二进制文件的完整路径将包含在所有输出消息中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/os</strong></p></td>
<td align="left"><p>符号的完整路径将包含在所有输出消息中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/Oc</strong> <em>目录</em></p></td>
<td align="left"><p>SymChk 将在 directory 目录中创建 <em>传统的符号</em> 树，其中包含已检查的所有符号文件的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/ov</strong></p></td>
<td align="left"><p>SymChk 还会打印已检查二进制文件的版本信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/Ol</strong> <em>文件</em></p></td>
<td align="left"><p>除了发送到标准输出的消息以外，还可以编写一个文件，其中包含以逗号分隔的所有二进制文件及其符号的列表。</p></td>
</tr>
</tbody>
</table>

 

**DBG 文件选项。** 这些选项控制 SymChk 如何检查 *dbg* 符号文件。 只能指定以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ds</strong></p></td>
<td align="left"><p>SymChk 将验证是否从可执行文件中去除了 dbg 信息，并且该信息仅出现在 dbg 文件中，并且可执行文件指向 dbg 文件。 如果程序是在不包含 dbg 符号文件的情况下生成的，则此选项不起作用。 这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/de</strong></p></td>
<td align="left"><p>SymChk 将验证是否未从可执行文件中去除 dbg 信息，并且可执行文件不会指向一个 dbg 文件。 如果程序是在不包含 dbg 符号文件的情况下生成的，则此选项不起作用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/dn</strong></p></td>
<td align="left"><p>SymChk 将验证此图像中是否不存在 dbg 信息，并且该图像是否未指向一个 dbg 文件。</p></td>
</tr>
</tbody>
</table>

 

**PDB 文件选项。** 这些选项控制 SymChk 如何检查 .pdb 符号文件。 只能指定以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/pf</strong></p></td>
<td align="left"><p>SymChk 不会对 .pdb 文件的内容执行任何检查，只需验证文件是否存在并与二进制文件匹配。 这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/ps</strong></p></td>
<td align="left"><p>SymChk 将验证是否已去掉了源行、数据类型和全局信息的 .pdb 文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/pt</strong></p></td>
<td align="left"><p>SymChk 将验证 .pdb 文件是否包含数据类型信息。</p></td>
</tr>
</tbody>
</table>

 

**筛选选项。** 这些选项控制 SymChk 检查进程或转储文件时执行模块筛选的方式。 只能指定以下选项之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/Fm</strong> <em>模块</em></p></td>
<td align="left"><p>SymChk 只会检查转储文件或与指定模块关联的进程。 <em>模块</em> 必须包含完整文件名，但不得包含目录路径的任何部分。</p></td>
</tr>
</tbody>
</table>

 

**符号检查选项。** 可以指定下列任意数量的选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/cs</strong></p></td>
<td align="left"><p>SymChk 不会验证 CodeView 数据是否存在。  (默认情况下，将验证是否存在 CodeView 数据。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/cc</strong></p></td>
<td align="left"><p>当 SymChk 检查修补程序 CAB 文件时，它不会在 CAB 内查找符号。  (默认情况下，SymChk 将在 cab 以及提供的符号路径中查找符号。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/Ea</strong> <em>文件</em></p></td>
<td align="left"><p>SymChk 不会验证指定文件中列出的程序的符号。 这允许您否决某些程序，否则会进行验证。 <em>文件</em> 必须仅指定一个文件 (按相对路径、绝对路径或 UNC 路径，但不) 通配符;如果包含空格，则应该用引号将其引起来。 在 <em>文件</em>中，每行表示一个程序文件 (按相对路径、绝对路径或 UNC 路径) ;不允许使用通配符。 如果此文件中的行包含空格，则应将其括在引号中。 此文件中的分号是注释字符，在分号与行尾之间的所有内容都将被忽略。 如果正在使用符号服务器，则不会将这些程序的符号复制到下游存储区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/Ee</strong> <em>文件</em></p></td>
<td align="left"><p>将禁止显示在指定文件中列出的程序的错误消息。 "成功" 和 "忽略" 消息将照常显示，符号文件将照常复制到下游存储。 <em>文件</em>的格式和其内容的格式与<strong>/ea</strong> <em>文件</em>的格式相同。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 SymChk 的详细信息，请参阅 [使用 SymChk](using-symchk.md)。

 

 





