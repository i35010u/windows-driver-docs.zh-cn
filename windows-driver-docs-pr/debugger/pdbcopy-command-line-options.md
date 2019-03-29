---
title: PDBCopy 命令行选项
description: PDBCopy 命令行使用以下语法。 可以按任意顺序包含参数。
ms.assetid: a793f860-db21-41fb-a0d2-931812400f0d
keywords:
- PDBCopy 命令行选项 Windows 调试
ms.date: 04/10/2018
topic_type:
- apiref
api_name:
- PDBCopy Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9f8c1ed1d96b0bc9654ce5ce9aa26cd0c8c04d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569364"
---
# <a name="pdbcopy-command-line-options"></a>PDBCopy 命令行选项


PDBCopy 命令行使用以下语法。 可以按任意顺序包含参数。

```dbgcmd
pdbcopy OldPDB NewPDB [Options] 

pdbcopy OldPDB NewPDB -p [-f:Symbol] [-f:@TextFile] [Options] 

pdbcopy OldPDB NewPDB -p [-F:Symbol] [-F:@TextFile] [Options] 

pdbcopy InputPDB BackupPDB -CVE-2018-1037 [autofix|verbose]

pdbcopy /? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______OldPDB______"></span><span id="_______oldpdb______"></span><span id="_______OLDPDB______"></span> *OldPDB*   
指定要读取的原始符号文件的路径和文件名称，其中包括.pdb 文件扩展名。 *OldPDB*可能包含本地计算机上的目录的绝对或相对路径或 UNC 路径。 如果指定没有路径，则使用当前工作目录。 如果*OldPDB*包含空格，则必须用引号引起来。

<span id="_______NewPDB______"></span><span id="_______newpdb______"></span><span id="_______NEWPDB______"></span> *NewPDB*   
指定要创建新符号文件的路径和文件名称，其中包括.pdb 文件扩展名。 *NewPDB*可能包含本地计算机上的目录的绝对或相对路径或 UNC 路径。 此路径必须已经存在;PDBCopy 将创建一个新目录。 如果指定没有路径，则使用当前工作目录。 如果*NewPDB*包含空格，则必须将其括在引号中。 指定的文件应不存在;如果是这样，新的文件无法写入，或可能编写不正确。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
若要从新的符号文件中删除私有符号数据的原因 PDBCopy。 如果旧的符号文件包含没有私有符号，则此选项无效。 如果省略此选项，则 PDBCopy 创建相同的符号的内容的新文件与原始文件。

<span id="-f_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-f:**<em>符号</em>  
导致 PDBCopy 从新的符号文件中删除指定的公共符号。 *符号*必须指定要删除的符号名称，包括任何符号名称修饰 （例如，初始下划线），但不是包括模块名称。 此选项需要-p 选项。 如果使用了多个 **-f**或 **-f: @** 参数，PDBCopy 从新的符号文件中移除所有指定的符号。

<span id="-f__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-f:@**<em>TextFile</em>  
导致 PDBCopy 若要删除新的符号文件中指定的文本文件中列出的公共符号。 *TextFile*指定文件名和路径 （绝对或相对） 的此文件。 此文件可以列出的任意数量的符号，一个在每个行，包括任何符号名称修饰 （例如，初始下划线），但不是包括模块名称的名称。 此选项需要-p 选项。

<span id="-F_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-F:**<em>符号</em>  
若要从新的符号文件，除了指定公共符号中删除所有公共和私有符号的原因 PDBCopy。 *符号*必须指定要保留符号的名称，包括任何符号名称修饰 （例如，初始下划线），但不是包括模块名称。 此选项需要-p 选项。 如果多个 **-F**或 **-f: @** 使用参数，所有指定的符号都保留在新的符号文件。

<span id="-F__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-F:@**<em>TextFile</em>  
导致 PDBCopy 从新的符号文件，除了指定的文本文件中列出的公共符号中删除所有公共和私有符号。 *TextFile*指定文件名和路径 （绝对或相对） 的此文件。 此文件可以列出的任意数量的符号，一个在每个行，包括任何符号名称修饰 （例如，初始下划线），但不是包括模块名称的名称。 此选项需要-p 选项。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项的任意组合。 这些选项是区分大小写。

<span id="-s"></span><span id="-S"></span>**-s**  
将导致新的符号文件，与旧的文件具有不同的签名。 通常您不应使用-s 选项，因为一个新的签名可能会导致 SymSrv 将不同的索引值分配到新的文件比旧的文件，防止正确替换旧的一个新的文件。

<span id="-vc6"></span><span id="-VC6"></span>**-vc6**  
若要使用而不是 mspdb80.dll mspdb60.dll 的原因 PDBCopy。 此选项从来不是必需的因为 PDBCopy 将自动查找正确版本的 mspdb\*.dll。 默认情况下，PDBCopy 使用 mspdb80.dll，这是使用 Visual Studio.NET 2002年和更高版本的 Visual Studio 的版本。 如果使用 Visual Studio 6.0 或早期版本生成您自己的符号，可以指定此命令行选项，以确保 PDBCopy 将改为使用 mspdb60.dll。 但是，这不是必需，因为 PDBCopy 查找合适的文件，即使不使用此选项。 任何版本的 mspdb\*.dll 使用必须在命令提示符窗口，则启动 PDBCopy 的可执行文件的路径。


<span id="CVE-2018-1037"></span> **-CVE-2018-1037**   

报告是否 InputPDBFile 具有 CVE-2018-1037年中所述的问题，并且可以选择修正此问题。 请参阅[KB # 4131751-PDBCopy 工具](https://support.microsoft.com/help/4131751/pdbcopy-update-to-fix-pdb-security-issue)有关详细信息和详细使用情况信息。


<span id="_______-_______"></span> **-?**   
显示帮助文本 PDBCopy 命令行。



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 PDBCopy 工具的详细信息，请参阅[使用 PDBCopy](using-pdbcopy.md)。

 

 





