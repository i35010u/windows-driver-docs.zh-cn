---
title: BinPlace 目标目录
description: BinPlace 目标目录
ms.assetid: 7a5a2324-b2a1-488b-b8de-cb5a6319d3ec
keywords:
- BinPlace WDK，目标目录
- 目标目录 WDK BinPlace
- 符号根目录 WDK BinPlace
- 类子目录 WDK BinPlace
- 文件类型子目录 WDK BinPlace
- 将文件 WDK BinPlace 放
- 目录 WDK BinPlace
- 符号文件 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff36360cd8e4aa49448a9a01d684f37144de4e5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351474"
---
# <a name="binplace-destination-directories"></a>BinPlace 目标目录


## <span id="ddk_binplace_destination_directories_tools"></span><span id="DDK_BINPLACE_DESTINATION_DIRECTORIES_TOOLS"></span>


BinPlace 创建目录树，以保存正在设置的文件。 该树的结构由传递给 BinPlace 的命令行中，某些环境变量，值并且名为文本文件的内容的参数*位置文件*。

BinPlace 将放置文件，如果满足两个条件之一：

1.  在 BinPlace 命令行上指定的文件。

2.  该文件是驻留在与它关联的可执行文件相同的目录中的符号文件和命令行上指定的可执行文件。 在这种情况下，符号文件的可执行文件将放置在不同的目录中。 BinPlace 还可以执行拆分或最小化 (请参阅[公共符号和私有符号](public-symbols-and-private-symbols.md)) 或最小化 (请参阅[符号的文件系统](symbol-file-systems.md)) 在此方案中。

当 BinPlace 将放入文件时，它将自动覆盖具有相同名称的较旧的文件。 但是，BinPlace 不会默认情况下覆盖较新的文件。 具体而言，如果存在可执行文件的更高版本 （或相同） 版本，则可执行文件和任何关联的符号文件都不会写入磁盘。 如果你想 BinPlace 覆盖文件而不考虑其时间戳，使用 **-f**命令行选项。

### <a name="span-idfiledestinationsspanspan-idfiledestinationsspanfile-destinations"></a><span id="file_destinations"></span><span id="FILE_DESTINATIONS"></span>文件目标

通过串联两个目录创建在其中 BinPlace 将放置在其命令行上指定的任何文件的目录的名称：*根目标目录*并*类子目录*。 （目录可以包含您选择的任何名称但根目标目录通常是其中要放置你的文件，类子目录是一个子目录其中合乎逻辑，将特定文件组放置在目录树的根.)

-   可以通过使用-r RootDestinationPath 命令行参数指定的根目标目录。 如果省略，默认值由\_NT386TREE， \_NTIA64TREE，或\_NTAMD64TREE 环境变量在基于 x86 的、 基于 Itanium 或基于 x64 的计算机上，分别。 必须在以下一种方式; 中定义的根目标目录如果未完全定义，将不会运行 BinPlace。

-   类子目录通常是位置文件中指定的。 可以指定一个文件; 的多个类子目录这将导致 BinPlace 使该文件的副本并将它们放在每个指定的位置。 请参阅[**位置文件语法**](place-file-syntax.md)有关完整详细信息。 此外可以通过使用指定的类子目录-: DEST 类路径中的命令行参数。

### <a name="span-idsymbolfiledestinationsspanspan-idsymbolfiledestinationsspansymbol-file-destinations"></a><span id="symbol_file_destinations"></span><span id="SYMBOL_FILE_DESTINATIONS"></span>符号文件目标

如果 BinPlace 的命令行上列出的可执行文件，则相同的目录中有一个关联的符号文件 BinPlace 将复制 （或 alter） 符号文件。 通过连接三个目录创建在其中放置此符号文件的目录：*符号根目录*，则*类子目录*，和*文件类型的子目录*.

-   可以通过使用-s SymbolRoot 命令行参数指定的符号的根目录。 如果使用的 **-a**并 **-x**开关，去除的符号文件将置于下*SymbolRoot*目录--在这种情况下，您可以使用-n FullSymbolRoot 指定完整的符号文件的位置。

-   类子目录通常是位置文件中指定的。 可以指定一个文件; 的多个类子目录这将导致 BinPlace 使该文件的副本并将它们放在每个指定的位置。 请参阅[**位置文件语法**](place-file-syntax.md)有关完整详细信息。 此外可以通过使用指定的类子目录-: DEST 类路径中的命令行参数。 如果 **-y**使用命令行开关，任何类子目录用于符号文件-目标目录只需将包含的符号的根目录和文件类型子目录。

-   文件类型子目录仅用于符号文件。 它取决于原始的可执行文件的文件扩展名。 因此，与.exe 文件相关联的符号文件将被放置在 exe 子目录、 与 Dll 相关联的符号文件将放置在一个 dll 子目录，并与驱动程序相关联的符号文件将被放置在 sys 子目录中。 此约定可帮助避免名称冲突的文件--例如，myprogram.exe 和 myprogram.dll 可能都具有名为 myprogram.pdb，符号文件，但是这些符号文件将放置在不同子目录中。

没有为此算法的一个例外。 如果既没有 **-s**也不 **-n**是提供，完整的符号文件将被置于二进制文件所在的同一位置。

**请注意**   BinPlace 如果列出 BinPlace 的命令行中的符号文件名称，则会移动它类似于任何其他文件和不检查其内容。 若要使用 BinPlace 的符号文件操作技巧，则必须列出可执行文件名称，而不是符号文件名称。

 

 

 





