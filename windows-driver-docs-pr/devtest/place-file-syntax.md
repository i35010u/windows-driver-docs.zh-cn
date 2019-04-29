---
title: 位置文件语法
description: 位置文件是 BinPlace 读取它以确定它正在设置的文件与相关联的类子目录的文本文件。
ms.assetid: 49f58ed1-9a4d-4e3e-9248-eebd95271374
keywords:
- 放置文件语法的驱动程序开发工具
topic_type:
- apiref
api_name:
- Place File Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c01f47bb90f157ac4e2b411f006bf553ff4211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356318"
---
# <a name="place-file-syntax"></a>位置文件语法


**请注意**文件现在已过时，并且不应使用。 .



位置文件是 BinPlace 读取它以确定它正在设置的文件与相关联的类子目录的文本文件。

-P PlaceFile 命令行参数指定的路径和该文件的名称。 如果未使用，默认值是\\工具\\placefil.txt。 位置文件可以有任意数量的行。 每一行都会列出一个文件和类子目录。 列出文件不会导致 BinPlace 需采取任何措施。 相反，每当 BinPlace 提供命令行上的文件名称，打开要查看是否列出了该文件的位置文件。 如果是，BinPlace 将使用该特定文件的位置文件中指定的类子目录。

位置文件的每一行都具有相同的格式。

```

     FileName Class[:Class[...]   [ ; Comment ] 
```

位置文件中的每一行遵循以下规则：

-   *文件名*字段必须以行。
-   *文件名*并*类*必须由一个或多个空格分隔的字段。
-   如果分号行上任意位置出现，它的右侧的所有内容被视为注释。
-   允许使用空的行和用分号开头的注释行。

*文件名*并*类*字段进行了说明，如下所示：

## <a name="span-idddkplacefilesyntaxtoolsspanspan-idddkplacefilesyntaxtoolsspanparameters"></a><span id="ddk_place_file_syntax_tools"></span><span id="DDK_PLACE_FILE_SYNTAX_TOOLS"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
一个字段，指定 BinPlace 可操作的文件的名称。 *文件名*必须包括文件扩展名，但它不能包含文件路径。 （文件路径将指定 BinPlace 命令行上。）

<span id="_______Class______"></span><span id="_______class______"></span><span id="_______CLASS______"></span> *类*   
一个字段，指定用于此文件的类子目录。 除非 **-y**或 **-: DEST**使用命令行开关，BinPlace 来将文件放在由根目标目录，目录中并追加类子目录，然后追加的文件类型的子目录。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)有关完整详细信息。

*类*应既不开始也不以反斜杠结尾。 目录名称不得包含空格。 可以在中使用的特殊字符串*类*值。 可执行文件和符号文件的位置位于不同的字符串的效果。 下表显示这些字符串的结果。

对于所有生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符串</th>
<th align="left">对可执行文件的影响</th>
<th align="left">影响符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>retail</strong></p></td>
<td align="left"><p>忽略。 将跳过该目录。</p></td>
<td align="left"><p>一个名为的文本目录被视为<strong>零售</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p></p>
在 x86 计算机： <strong>i386</strong>。
在基于 Itanium 的计算机：<strong>IA64</strong>。
在基于 x64 的计算机：<strong>AMD64</strong>。</td>
<td align="left"><p>忽略。 将跳过该目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>system</strong></p></td>
<td align="left"><p>将成为<strong>system32</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>system16</strong></p></td>
<td align="left"><p>将成为<strong>系统</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>windows</strong></p></td>
<td align="left"><p>将成为"。"忽略。 将跳过该目录。</p></td>
<td align="left"><p>符号路径是<strong>零售</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>drivers</strong></p></td>
<td align="left"><p>将成为<strong>system32\drivers</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>drvetc</strong></p></td>
<td align="left"><p>将成为<strong>system32\drivers\etc</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>config</strong></p></td>
<td align="left"><p>将成为<strong>system32\config</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



为 x86 生成：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符串</th>
<th align="left">对可执行文件的影响</th>
<th align="left">影响符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>将成为<strong>system32</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>printer</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\drivers\w32x86</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\prtprocs\w32x86</strong>。</p></td>
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
<th align="left">字符串</th>
<th align="left">对可执行文件的影响</th>
<th align="left">影响符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>将成为"<strong>...</strong>"例如，如果根目标目录为 C:\Binaries\Amd64，该文件位于 C:\Binaries。</p></td>
<td align="left"><p>符号路径剔除的一个目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>printer</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\drivers\w32amd64</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\prtprocs\w32amd64</strong>。</p></td>
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
<th align="left">字符串</th>
<th align="left">对可执行文件的影响</th>
<th align="left">影响符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>将成为"<strong>...</strong>"</p></td>
<td align="left"><p>符号路径剔除的一个目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>printer</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\drivers\w32ia64</strong>。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>prtprocs</strong></p></td>
<td align="left"><p>将成为<strong>system32\spool\prtprocs\w32ia64</strong>。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>



除非另行说明，否则被截断的符号路径，以仅包含第一个目录路径中。 例如，如果你已使用 BinPlace 移动 x86 文件调用具有的目标类的 Build.exe**打印机**，可以使用以下命令语法：

```
binplace -r BinaryRoot  -xa -s SymbolsDir1 -n SymbolsDir2 SourceFileLocation\build.exe
```

该命令将导致以下输出目录树：

```
<SymbolsDir1>\system32\exe\build.pdb
<SymbolsDir2>\system32\exe\build.pdb 
<BinaryRoot>\system32\spool\drivers\w32x86\build.exe 
```

对于 AMD64 和 IA64 版本中，使用**hal**类谨慎，因为 BinPlace 结果可能不是你期望的内容。 例如，如果根目标目录为 c:\\二进制文件\\Amd64，和你指定**hal**类，该文件位于 c:\\二进制文件而不是在特定的处理器的目录，你可能已考虑。

如果你想要放置在多个位置的文件，可以包括多个实例*类*、 由冒号分隔。 不能有目录和冒号之间的空格。 例如：

```
someprogram.exe   dir1\dir2\dir3:otherdir1\otherdir2   ; To two locations
```

<span id="_______Comment______"></span><span id="_______comment______"></span><span id="_______COMMENT______"></span> *注释*   
BinPlace 将忽略分号后的任何文本。









