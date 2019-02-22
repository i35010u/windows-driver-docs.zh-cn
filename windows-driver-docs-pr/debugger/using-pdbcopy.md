---
title: 使用 PDBCopy
description: 使用 PDBCopy
ms.assetid: f8207b09-5a1b-4ff3-b99d-20daa88cfe10
keywords:
- PDBCopy，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f5d61816aa99cb20dd7c91db0f2ca4ba266b12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523188"
---
# <a name="using-pdbcopy"></a>使用 PDBCopy


PDBCopy 是一个命令行工具，通过完整符号文件创建去除的符号文件。 换句话说，需要符号文件，包含私有符号数据和公共符号表，并创建该文件包含仅公共符号表的副本。 根据使用的 PDBCopy 选项，去除的符号文件将包含整个公共符号表或指定公共符号表的子集。

PDBCopy 适用于任何 PDB 格式符号文件 （带有文件名称扩展.pdb)，但不能与较旧的格式 (.dbg) 符号文件。

公共符号表和私有符号数据的说明，请参阅[公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idremovingprivatesymbolsspanspan-idremovingprivatesymbolsspanremoving-private-symbols"></a><span id="removing_private_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS"></span>删除私有符号

如果你想要创建包含所有公共符号和无私有符号的去除的符号文件，使用 PDBCopy 具有三个参数： 的路径和名称的原始符号文件、 路径和名称以及新的符号文件中，-p 选项。

例如，以下命令创建名为 publicsymbols.pdb，其中包含与 mysymbols.pdb 相同的公共符号表，但其中不包含任何私有符号数据的新文件：

**pdbcopy mysymbols.pdb publicsymbols.pdb -p**

如果 mysymbols.pdb 碰巧已去除的符号文件，新的文件和旧文件的符号的内容将是相同的。

发出该命令后, 你应将新文件移到新位置，并重命名为符号文件的原始名称 (在此示例中，mysymbols.pdb)，因为大多数调试程序符号提取程序查找基于特定文件的符号名称。 或者，可以使用相同的文件名的输入的文件和输出文件上 PDBCopy 命令行中，只要指定了不同的目录：

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir2\\mysymbols.pdb -p**

**请注意**  PDBCopy 运行之前，不应存在目标文件。 如果存在具有此名称的文件，可能会发生各种错误。

 

### <a name="span-idremovingprivatesymbolsandselectedpublicsymbolsspanspan-idremovingprivatesymbolsandselectedpublicsymbolsspanremoving-private-symbols-and-selected-public-symbols"></a><span id="removing_private_symbols_and_selected_public_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS_AND_SELECTED_PUBLIC_SYMBOLS"></span>删除私有符号和所选公共符号

如果你想要不只删除私有符号数据中，而且还减少的公共符号表中的信息，可以使用-f 选项以指定要从中删除的公共符号的列表。

下面的示例说明了此过程：

1.  确定的完整名称，包括修饰，你想要删除的符号。 如果您不确定的修饰的符号名称，则可以使用[DBH](dbh.md)工具来确定它们。 请查看来确定特定的符号，有关详细信息的修饰。 在此示例中，让我们假设你想要删除的符号的修饰的名是 **\_myGlobal1**并 **\_myGlobal2**。

2.  创建包含要删除的符号的列表的文本文件。 此文件中的每行应包含一个符号，包括修饰，但不是包括模块名称的名称。 在此示例中，该文件将包含以下两行：

    ```text
    _myGlobal1
    _myGlobal2 
    ```

    您选择的任何名称，可以指定文件。 让我们假设命名此文件 listfile.txt，并将其放在目录 c:\\Temp。

3.  使用以下 PDBCopy 命令行：

    ```console
    pdbcopy OldPDB NewPDB-p -f:@TextFile 
    ```

    其中*OldPDB*并*NewPDB*是原始的符号文件和新的符号文件，并*TextFile*是第二步中创建的文件。 -F 选项表示某些公共符号将被删除，& 符 （@） 表示，这些符号会列出在指定的文本文件中。

    在当前示例中，该命令将如下所示：

    ```console
    pdbcopy c:\dir1\mysymbols.pdb c:\dir3\mysymbols.pdb -p -f:@c:\temp\listfile.txt 
    ```

    这将创建新的符号文件，c:\\dir2\\mysymbols.pdb，它不包含任何私有符号并不包含 listfile.txt 中列出的两个全局变量。

此示例中所示，PDBCopy 的-f 选项删除公共符号的特定列表。 & 符 （@） 表示，这些符号会在文本文件中列出。 另一种方法是列出使用-f 选项而无需与号在命令行上的所有符号。 因此下面的命令行等效于上述过程中的示例：

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir3\\mysymbols.pdb -p -f:\_myGlobal1 -f:\_myGlobal2**

除非你想要删除一个或两个符号，它会使用比若要列出其命令行上的文本文件更为简单。

如果你想要从.pdb 文件中删除的大部分公共符号，-F 选项是最简单的方法。 -F 选项要求您列出你想要删除这些公共符号，而-F 选项要求列出你不想要删除这些公共符号。 将删除所有其他公共符号 （以及所有私有符号）。 -F 选项支持-f 选项与相同的两个语法选项:-符号的名称后跟的 f： 要保留或-f: @ 跟包含要保留的符号的列表的文本文件的名称。 在任一情况下，修饰，必须使用名称的符号。

例如，以下命令将删除所有私有符号和几乎所有的公共符号，离开仅符号 **\_myFunction5**并 **\_myGlobal7**:

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir3\\mysymbols.pdb -p -F:\_myFunction5 -F:\_myGlobal7**

如果将组合在同一行-f 选项的多个实例时，会删除所有指定的符号。 如果将结合使用-F 选项在同一行的多个实例，所有指定的字符被保留，并删除所有其他符号。 不能将-f 组合使用。

-F 和-F 选项不能使用但不使用-p 选项，删除所有专用符号数据。 即使原始文件包含没有私有符号，则必须包含-p 选项 （尽管它在这种情况下没有任何影响）。

-F 选项不能用于防止私有符号的数据被删除。 如果不包含公共符号表中的符号与使用此选项，PDBCopy 将其忽略。

### <a name="span-idthemspdbdllfilespanspan-idthemspdbdllfilespanthe-mspdbdll-file"></a><span id="the_mspdb__dll_file"></span><span id="THE_MSPDB__DLL_FILE"></span>Mspdb\*.dll 文件

PDBCopy 必须访问 Mspdb80.dll 文件或 Mspdb60.dll 文件才能运行。 默认情况下，PDBCopy 使用 Mspdb80.dll，这是使用 Visual Studio.NET 2002年和更高版本的 Visual Studio 的版本。 如果使用 Visual Studio 6.0 或早期版本生成您自己的符号，可以指定使该 PDBCopy 使用 Mspdb60.dll 相反，尽管这不是必需的-vc6 命令行选项。 PDBCopy 查找相应的文件即使-vc6 不使用选项。 您可以在您安装的 Visual Studio、 Platform SDK 或 Windows Driver Kit (WDK) 中找到这些文件。

在运行之前 PDBCopy，确保正确版本的 mspdb\*.dll 文件可以访问您的计算机，并确保其位置的命令路径的一部分。 如果不存在，则应使用**路径**命令将此位置添加到命令路径。

### <a name="span-idthefilesignatureandthesymsrvindexspanspan-idthefilesignatureandthesymsrvindexspanthe-file-signature-and-the-symsrv-index"></a><span id="the_file_signature_and_the_symsrv_index"></span><span id="THE_FILE_SIGNATURE_AND_THE_SYMSRV_INDEX"></span>文件签名和 SymSrv 索引

每个符号文件包含唯一标识它的固定的签名。 SymSrv 使用签名生成唯一"索引值"的文件。 如果两个文件具有不同的内容或不同的创建时间，则也会区分不同的签名和非重复 SymSrv 索引值。

使用 PDBCopy 创建的文件是唯一的索引值的规则的例外。 当 PDBCopy 创建一个新的符号文件时，它具有与旧的文件相同的签名和 SymSrv 索引值。 此功能，而无需更改符号相关的工具的行为将替换为另一个文件。

如果你想要具有不同的签名和 SymSrv 索引的新文件，请使用-s 选项。 在大多数情况下将不希望使用此选项，因为 PDBCopy 的最常见用途是创建可以替换旧文件而不会导致不匹配的更改后的符号文件。 一个新的签名可能会导致 SymSrv 将不同的索引值分配到比旧的文件，防止新的文件正确替换旧到新的文件。

有关完整的命令行语法，请参阅[ **PDBCopy 命令行选项**](pdbcopy-command-line-options.md)。

 

 





