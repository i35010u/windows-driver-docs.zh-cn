---
title: 使用 PDBCopy
description: 使用 PDBCopy
keywords:
- Pdbcopy.exe，使用
ms.date: 10/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: f60983657028a0bb3861bbe1c445a78f029e908e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803083"
---
# <a name="using-pdbcopy"></a>使用 PDBCopy

Pdbcopy.exe 是一个命令行工具，可从完整的符号文件创建一个去除的符号文件。 换言之，它采用一个包含 private 符号数据和一个公共符号表的符号文件，并创建该文件的副本，该副本只包含公共符号表。 根据所使用的 Pdbcopy.exe 选项，去除的符号文件包含整个公共符号表或公共符号表的指定子集。

有关 WDK 中 Pdbcopy.exe 的位置，请参阅 [Windows 调试工具中包含的工具](extra-tools.md#installation-directory)中的 **安装目录**。

Pdbcopy.exe 使用文件扩展名为 .pdb)  (任何 PDB 格式的符号文件，但不能使用旧格式 ( dbg) 符号文件。

有关公共符号表和私有符号数据的说明，请参阅 [公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idremoving_private_symbolsspanspan-idremoving_private_symbolsspanremoving-private-symbols"></a><span id="removing_private_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS"></span>删除私有符号

如果你想要创建包含所有公共符号且不包含任何私有符号的去除符号文件，请使用带有三个参数的 Pdbcopy.exe：原始符号文件的路径和名称、新符号文件的路径和名称以及-p 选项。

例如，以下命令将创建名为 publicsymbols 的新文件，该文件包含与 mysymbols 相同的公共符号表，但不包含任何私有符号数据：

**pdbcopy.exe mysymbols publicsymbols-p**

如果 mysymbols 已是一个去除符号文件，则新文件和旧文件的符号内容将相同。

发出此命令后，应将新文件移到新位置，并将其重命名为符号文件的原始名称 (在此示例中，mysymbols) ，因为大多数调试程序和符号提取程序会根据特定的文件名查找符号。 或者，只要指定了不同的目录，也可以在 Pdbcopy.exe 命令行上对输入文件和输出文件使用相同的文件名：

**pdbcopy.exe c： \\ dir1 \\ mysymbols： \\ dir2 \\ mysymbols-p**

**注意**  在运行 Pdbcopy.exe 之前，目标文件应不存在。 如果存在具有此名称的文件，则可能会发生各种错误。

### <a name="span-idremoving_private_symbols_and_selected_public_symbolsspanspan-idremoving_private_symbols_and_selected_public_symbolsspanremoving-private-symbols-and-selected-public-symbols"></a><span id="removing_private_symbols_and_selected_public_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS_AND_SELECTED_PUBLIC_SYMBOLS"></span>删除私有符号和选定的公共符号

如果希望不仅删除私有符号数据，还希望减少公共符号表中的信息量，可以使用-f 选项来指定要删除的公共符号列表。

下面的示例演示了此过程：

1. 确定要删除的符号的完整名称，包括修饰。 如果你不确定修饰符号名称，则可以使用 [this->dbh](dbh.md) 工具来确定它们。 有关详细信息，请参阅确定特定符号的修饰。 在此示例中，我们假设要删除的符号的修饰名是 **\_ myGlobal1** 和 **\_ myGlobal2**。

2. 创建一个文本文件，其中包含要删除的符号列表。 此文件中的每行应包含一个符号（包括修饰）的名称，但不包含模块名称。 在此示例中，该文件将包含以下两行：

    ```text
    _myGlobal1
    _myGlobal2
    ```

    可以为该文件提供您选择的任何名称。 假设你将此文件命名为 listfile.txt，并将其放入目录 C： \\ Temp。

3. 使用以下 Pdbcopy.exe 命令行：

    ```console
    pdbcopy OldPDB NewPDB -p -f:@TextFile
    ```

    其中 *OldPDB* 和 *NewPDB* 是原始符号文件和新的符号文件，而 *TextFile* 是第二步中创建的文件。 -F 选项指示将删除某些公共符号，并 ( @ ) 指示这些符号在指定的文本文件中列出。

    在当前的示例中，命令将如下所示：

    ```console
    pdbcopy c:\dir1\mysymbols.pdb c:\dir3\mysymbols.pdb -p -f:@c:\temp\listfile.txt
    ```

    这将创建一个新的符号文件 C： \\ dir3 \\ mysymbols，它不包含任何私有符号，也不包含 listfile.txt 中列出的两个全局变量。

如本示例所示，Pdbcopy.exe 的-f 选项将删除特定的公共符号列表。 @ )  ( @ 符号指示这些符号在文本文件中列出。 另一种方法是在命令行上列出所有符号，使用不带 "and" 符的-f 选项。 因此，下面的命令行等效于上述过程中的示例：

**pdbcopy.exe c： \\ dir1 \\ mysymbols： \\ dir3 \\ mysymbols-p-f： \_ myGlobal1-f： \_ myGlobal2**

除非您只想删除一个或两个符号，否则使用文本文件比在命令行上列出它们更简单。

如果要从 .pdb 文件中删除大多数公共符号，则-F 选项是最简单的方法。 尽管-f 选项要求您列出要删除的公共符号，但-F 选项要求您列出不希望删除的公共符号。 将删除所有其他公共符号 (以及所有的私有符号) 。 -F 选项支持与-f 选项相同的两个语法选项：-F：-F：，后跟要保留的符号的名称，或者-F： @ 后跟包含要保留的符号列表的文本文件的名称。 在任一情况下，都必须使用修饰符号名称。

例如，以下命令将删除所有私有符号，几乎所有公共符号，只留下符号 **\_ myFunction5** 和 **\_ myGlobal7**：

**pdbcopy.exe c： \\ dir1 \\ mysymbols： \\ dir3 \\ Mysymbols-p-F： \_ myFunction5-f： \_ myGlobal7**

如果将-f 选项的多个实例合并到一行中，则删除所有指定的符号。 如果将-F 选项的多个实例合并到一行上，则将保留所有指定的符号，并删除所有其他符号。 不能将-f 和-F 组合在一起。

如果不使用-p 选项，则不能使用-f 和-F 选项，这将删除所有私有符号数据。 即使原始文件不包含私有符号，也仍然必须包含-p 选项 (但在这种情况下不会产生任何影响) 。

-F 选项不能用于防止删除私有符号数据。 如果将此选项与公共符号表中不包含的符号一起使用，则 Pdbcopy.exe 将忽略它。

### <a name="span-idthe_mspdb__dll_filespanspan-idthe_mspdb__dll_filespanthe-mspdbdll-file"></a><span id="the_mspdb__dll_file"></span><span id="THE_MSPDB__DLL_FILE"></span>Mspdb \* 文件

Pdbcopy.exe 必须访问 Mspdb80.dll 文件或 Mspdb60.dll 文件才能运行。 默认情况下，Pdbcopy.exe 使用 Mspdb80.dll，这是 Visual Studio .NET 2002 和更高版本的 Visual Studio 使用的版本。 如果你的符号是使用 Visual Studio 6.0 或更早版本生成的，则可以指定-vc6.dll 命令行选项，以便 Pdbcopy.exe 改用 Mspdb60.dll，尽管这不是必需的。 即使未使用-vc6.dll 选项，Pdbcopy.exe 也会查找相应的文件。 可以在安装的 Visual Studio、平台 SDK 或 Windows 驱动程序工具包 (WDK) 中找到这些文件。

在运行 Pdbcopy.exe 之前，请确保 \* 计算机可以访问 mspdb 文件的正确版本，并确保其位置是命令路径的一部分。 如果不是，则应使用 **path** 命令将此位置添加到命令路径。

### <a name="span-idthe_file_signature_and_the_symsrv_indexspanspan-idthe_file_signature_and_the_symsrv_indexspanthe-file-signature-and-the-symsrv-index"></a><span id="the_file_signature_and_the_symsrv_index"></span><span id="THE_FILE_SIGNATURE_AND_THE_SYMSRV_INDEX"></span>文件签名和 SymSrv 索引

每个符号文件都有一个唯一标识它的固定签名。 SymSrv 使用签名为该文件生成唯一的 "索引值"。 如果两个文件的内容不同或创建时间不同，则它们还将具有不同的签名和不同的 SymSrv 索引值。

使用 Pdbcopy.exe 创建的文件是唯一索引值的规则的例外情况。 当 Pdbcopy.exe 创建新的符号文件时，它具有与旧文件相同的签名和 SymSrv 索引值。 此功能允许将一个文件替换为另一个文件，而无需更改与符号相关的工具的行为。

如果希望新文件具有不同的签名和 SymSrv 索引，请使用-s 选项。 在大多数情况下，你不希望使用此选项，因为 Pdbcopy.exe 最常见的用途是创建一个修改后的符号文件，该文件可替换旧文件而不会导致不匹配。 新签名可能会导致 SymSrv 为新文件分配不同于旧文件的索引值，从而阻止新文件正确替换旧文件。

有关完整的命令行语法，请参阅 [**pdbcopy.exe Command-Line 选项**](pdbcopy-command-line-options.md)。

 

 





