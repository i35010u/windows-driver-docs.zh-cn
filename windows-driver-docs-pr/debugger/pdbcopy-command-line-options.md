---
title: PDBCopy 命令行选项
description: Pdbcopy.exe 命令行使用以下语法。 可以按任意顺序包含参数。
keywords:
- Pdbcopy.exe Command-Line 选项 Windows 调试
ms.date: 04/10/2018
topic_type:
- apiref
api_name:
- PDBCopy Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e86d9a9174f7610faad89d6134fb23cf2f4f3b58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840831"
---
# <a name="pdbcopy-command-line-options"></a>PDBCopy 命令行选项


Pdbcopy.exe 命令行使用以下语法。 可以按任意顺序包含参数。

```dbgcmd
pdbcopy OldPDB NewPDB [Options] 

pdbcopy OldPDB NewPDB -p [-f:Symbol] [-f:@TextFile] [Options] 

pdbcopy OldPDB NewPDB -p [-F:Symbol] [-F:@TextFile] [Options] 

pdbcopy InputPDB BackupPDB -CVE-2018-1037 [autofix|verbose]

pdbcopy /? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______OldPDB______"></span><span id="_______oldpdb______"></span><span id="_______OLDPDB______"></span>*OldPDB*   
指定要读取的原始符号文件的路径和文件名，包括 .pdb 文件扩展名。 *OldPDB* 可能包含本地计算机上某个目录的绝对路径或相对路径或 UNC 路径。 如果未指定路径，则使用当前工作目录。 如果 *OldPDB* 包含空格，则必须用引号将其引起来。

<span id="_______NewPDB______"></span><span id="_______newpdb______"></span><span id="_______NEWPDB______"></span>*NewPDB*   
指定要创建的新符号文件的路径和文件名，包括 .pdb 文件扩展名。 *NewPDB* 可能包含本地计算机上某个目录的绝对路径或相对路径或 UNC 路径。 此路径必须已经存在;Pdbcopy.exe 不会创建新的目录。 如果未指定路径，则使用当前工作目录。 如果 *NewPDB* 包含空格，则必须用引号将其引起来。 指定的文件不应已存在;如果是这样，则可能无法写入新文件，或写入不正确。

<span id="_______-p______"></span><span id="_______-P______"></span>**-p**   
使 Pdbcopy.exe 从新的符号文件中删除私有符号数据。 如果旧的符号文件不包含私有符号，则此选项不起作用。 如果省略此选项，则 Pdbcopy.exe 将创建一个与原始文件具有相同符号内容的新文件。

<span id="-f_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-f：**<em>符号</em>  
使 Pdbcopy.exe 从新的符号文件中删除指定的公共符号。 *符号* 必须指定要删除的符号的名称，包括任何符号名称修饰 (例如，初始下划线) ，但不包括模块名称。 此选项需要-p 选项。 如果使用多个 **-f** 或 **-f： @** 参数，pdbcopy.exe 将从新的符号文件中删除所有指定的符号。

<span id="-f__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-f： @**<em>TextFile</em>  
使 Pdbcopy.exe 从新的符号文件中删除指定文本文件中列出的公共符号。 *TextFile* 指定文件的名称和路径 (绝对或相对) 。 此文件可以列出任意数量的符号名称，每行包含一个符号，其中每行包含符号名称修饰 (例如，初始下划线) ，但不包括模块名称。 此选项需要-p 选项。

<span id="-F_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-F：**<em>符号</em>  
使 Pdbcopy.exe 从新符号文件中删除所有公共和私有符号（指定的公共符号除外）。 *符号* 必须指定要保留的符号的名称，包括任何符号名称修饰 (例如，初始下划线) ，但不包括模块名称。 此选项需要-p 选项。 如果使用了多个 **F** 或 **-f： @** 参数，则所有指定的符号将保留在新的符号文件中。

<span id="-F__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-F： @**<em>TextFile</em>  
使 Pdbcopy.exe 从新符号文件中删除所有公共和私有符号，但指定的文本文件中列出的公共符号除外。 *TextFile* 指定文件的名称和路径 (绝对或相对) 。 此文件可以列出任意数量的符号名称，每行包含一个符号，其中每行包含符号名称修饰 (例如，初始下划线) ，但不包括模块名称。 此选项需要-p 选项。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下选项的任意组合。 这些选项区分大小写。

<span id="-s"></span><span id="-S"></span>**-s**  
导致新符号文件的签名与旧文件的签名不同。 通常不应使用-s 选项，因为新签名可能会导致 SymSrv 为新文件分配不同于旧文件的索引值，从而阻止新文件正确替换旧文件。

<span id="-vc6"></span><span id="-VC6"></span>**-vc6.dll**  
导致 Pdbcopy.exe 使用 mspdb60.dll 而不是 mspdb80.dll。 不需要此选项，因为 Pdbcopy.exe 会自动查找正确版本 \* 的 mspdb。 默认情况下，Pdbcopy.exe 使用 mspdb80.dll，这是 Visual Studio .NET 2002 和更高版本的 Visual Studio 使用的版本。 如果你的符号是使用 Visual Studio 6.0 或更早版本生成的，则可以指定此命令行选项，以便 Pdbcopy.exe 将改用 mspdb60.dll。 但这并不是必需的，因为即使未使用此选项，Pdbcopy.exe 也会查找相应的文件。 使用的任何版本的 mspdb \* 必须位于从中启动 pdbcopy.exe 的命令提示符窗口的可执行路径中。


<span id="CVE-2018-1037"></span>**-CVE-2018-1037**   

报告 InputPDBFile 是否具有 CVE-2018-1037 中描述的问题，并根据需要修正问题。 有关详细信息和使用情况信息，请参阅 [KB # 4131751-pdbcopy.exe 工具](https://support.microsoft.com/help/4131751/pdbcopy-update-to-fix-pdb-security-issue) 。


<span id="_______-_______"></span> **-?**   
显示 Pdbcopy.exe 命令行的帮助文本。



### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Pdbcopy.exe 工具的详细信息，请参阅 [使用 pdbcopy.exe](using-pdbcopy.md)。

 

 





