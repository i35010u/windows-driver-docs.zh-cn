---
title: 位置文件语法
description: 位置文件是一个 BinPlace 读取的文本文件，用于确定与该文件所放置的文件关联的类子目录。
keywords:
- 放置文件语法驱动程序开发工具
topic_type:
- apiref
api_name:
- Place File Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10f55301401af58038d6aa49f9fa707f9af548eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811129"
---
# <a name="place-file-syntax"></a>位置文件语法


**注意**   放置文件现在已过时，不应使用。 .



位置文件是一个 BinPlace 读取的文本文件，用于确定与该文件所放置的文件关联的类子目录。

此文件的路径和名称由-p PlaceFile 命令行参数指定。 如果未使用此值，则默认值为 \\ tools \\placefil.txt。 位置文件可以有任意数目的行。 每行都列出文件和类子目录。 列出文件不会导致 BinPlace 执行任何操作。 相反，每当在命令行上提供 BinPlace 时，它都会打开放置文件以查看是否列出了该文件。 如果是，BinPlace 将使用在该特定文件的位置文件中指定的类子目录。

位置文件的每一行都具有相同的格式。

```

     FileName Class[:Class[...]   [ ; Comment ] 
```

放置文件中的每一行都遵循以下规则：

-   *FileName* 字段必须以行开头。
-   *FileName* 和 *Class* 字段必须由一个或多个空格分隔。
-   如果行中的任何位置都出现分号，则将其右侧的所有内容都视为注释。
-   允许使用以分号开头的空白行和注释行。

" *文件名* " 和 " *类* " 字段的说明如下：

## <a name="span-idddk_place_file_syntax_toolsspanspan-idddk_place_file_syntax_toolsspanparameters"></a><span id="ddk_place_file_syntax_tools"></span><span id="DDK_PLACE_FILE_SYNTAX_TOOLS"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
一个字段，该字段指定 BinPlace 可以操作的文件的名称。 *FileName* 必须包含文件扩展名，但不得包含文件路径。 将在 BinPlace 命令行上指定 (文件路径。 ) 

<span id="_______Class______"></span><span id="_______class______"></span><span id="_______CLASS______"></span>*类*   
一个字段，该字段指定用于此文件的类子目录。 除非使用 **-y** 或 **-:D est** 命令行开关，否则，BinPlace 会将文件放在通过获取根目标目录创建的目录中，并追加类子目录，然后追加文件类型子目录。 有关完整详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

*类* 不应以反斜杠开头或结尾。 目录名称不能包含空格。 有一些特殊的字符串可在 *类* 值中使用。 字符串对可执行文件和符号文件的位置不同。 下表显示了这些字符串的结果。

对于所有生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">对可执行文件的影响</th>
<th align="left">对符号文件的影响</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>零售</strong></p></td>
<td align="left"><p>已忽略。 将跳过此目录级别。</p></td>
<td align="left"><p>被视为名为 <strong>retail</strong>的文本目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p></p>
在 x86 计算机上： <strong>i386</strong>。
在基于 Itanium 的计算机上： <strong>IA64</strong>。
在基于 x64 的计算机上： <strong>AMD64</strong>。</td>
<td align="left"><p>已忽略。 将跳过此目录级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>系统</strong></p></td>
<td align="left"><p>变为 <strong>system32</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>system16</strong></p></td>
<td align="left"><p>变为 <strong>系统</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>windows</strong></p></td>
<td align="left"><p>变为 ""。掉. 将跳过此目录级别。</p></td>
<td align="left"><p>符号路径为 <strong>零售</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>因素</strong></p></td>
<td align="left"><p>成为 <strong>system32\drivers</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>drvetc</strong></p></td>
<td align="left"><p>成为 <strong>system32\drivers\etc</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>config</strong></p></td>
<td align="left"><p>成为 <strong>system32\config</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



对于 x86 生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">对可执行文件的影响</th>
<th align="left">对符号文件的影响</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>变为 <strong>system32</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>打印机</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\drivers\w32x86</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\prtprocs\w32x86</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



对于 AMD64 生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">对可执行文件的影响</th>
<th align="left">对符号文件的影响</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>变为 "<strong>...</strong>"例如，如果根目标目录为 C:\Binaries\Amd64，则该文件位于 C:\Binaries. 中。</p></td>
<td align="left"><p>符号路径已去除一个目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>打印机</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\drivers\w32amd64</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\prtprocs\w32amd64</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



对于 IA64 生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">String</th>
<th align="left">对可执行文件的影响</th>
<th align="left">对符号文件的影响</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>变为 "<strong>...</strong>"</p></td>
<td align="left"><p>符号路径已去除一个目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>打印机</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\drivers\w32ia64</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>成为 <strong>system32\spool\prtprocs\w32ia64</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



除非另有说明，否则符号路径将被截断为仅包含路径中的第一个目录。 例如，如果使用 BinPlace 移动一个名为 Build.exe 的 x86 文件，该文件具有 **打印机** 的目标类，则可以使用以下命令语法：

```
binplace -r BinaryRoot  -xa -s SymbolsDir1 -n SymbolsDir2 SourceFileLocation\build.exe
```

命令将生成以下输出树：

```
<SymbolsDir1>\system32\exe\build.pdb
<SymbolsDir2>\system32\exe\build.pdb 
<BinaryRoot>\system32\spool\drivers\w32x86\build.exe 
```

对于 AMD64 和 IA64 版本，请谨慎使用 **hal** 类，因为 BinPlace 结果可能不是你所期望的结果。 例如，如果根目标目录为 C： \\ 二进制 \\ Amd64，并且您指定了 **hal** 类，则该文件将放在 C：二进制文件中， \\ 而不是位于您可能打算使用的特定目录中。

如果希望将文件放置在多个位置，可以包含 *类* 的多个实例，用冒号分隔。 目录和冒号之间不得有空格。 例如：

```
someprogram.exe   dir1\dir2\dir3:otherdir1\otherdir2   ; To two locations
```

<span id="_______Comment______"></span><span id="_______comment______"></span><span id="_______COMMENT______"></span>*注释*   
BinPlace 将忽略分号后面的任何文本。









