---
title: BinPlace 目标目录
description: BinPlace 目标目录
keywords:
- BinPlace WDK，目标目录
- 目标目录 WDK BinPlace
- 符号根目录 WDK BinPlace
- 类子目录 WDK BinPlace
- 文件类型子目录 WDK BinPlace
- 放置文件 WDK BinPlace
- 目录 WDK BinPlace
- 符号文件 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94b5ab47962a77f36182cdddc90879bd401dd6f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829699"
---
# <a name="binplace-destination-directories"></a>BinPlace 目标目录


## <span id="ddk_binplace_destination_directories_tools"></span><span id="DDK_BINPLACE_DESTINATION_DIRECTORIES_TOOLS"></span>


BinPlace 创建目录树以保存它所放置的文件。 该树的结构由传递给 BinPlace 的命令行的参数、某些环境变量的值和文本文件（称为 *位置文件*）的内容决定。

如果满足以下两个条件之一，BinPlace 将会放置文件：

1.  文件在 BinPlace 命令行上指定。

2.  文件是与关联的可执行文件位于同一目录中的符号文件，并在命令行中指定可执行文件。 在这种情况下，符号文件和可执行文件将放在不同的目录中。 BinPlace 也可以执行拆分或去除 (请参阅 [公共符号和私有符号](public-symbols-and-private-symbols.md)) 或去除 (参阅此方案中的 [符号文件系统](symbol-file-systems.md)) 。

当 BinPlace 放置文件时，它会自动覆盖具有相同名称的旧文件。 但是，默认情况下，BinPlace 将不会覆盖较新的文件。 特别是，如果存在可执行文件的较新 (或相同) 版本，则可执行文件和任何关联的符号文件都不会写入磁盘。 如果希望 BinPlace 无论其时间戳如何都覆盖文件，请使用 **-f** 命令行选项。

### <a name="span-idfile_destinationsspanspan-idfile_destinationsspanfile-destinations"></a><span id="file_destinations"></span><span id="FILE_DESTINATIONS"></span>文件目标

BinPlace 在其命令行上指定指定的任何文件的目录的名称是通过串联两个目录创建的： *根目标目录* 和 *类子目录*。  (目录可具有你选择的任何名称，但通常，根目标目录是要在其中放置文件的目录树的根，而类子目录则是一个子目录，在此子目录下，放置特定文件或文件组的逻辑。 ) 

-   可以使用-r RootDestinationPath 命令行参数指定根目标目录。 如果省略此值，则默认值由基于 \_ Itanium 的基于 \_ Itanium 的 \_ 计算机或基于 x64 的计算机上的 NT386TREE、NTIA64TREE 或 NTAMD64TREE 环境变量决定。 必须通过以下方式之一定义根目标目录;如果根本没有定义，BinPlace 将不会运行。

-   通常在位置文件中指定类子目录。 可以为一个文件指定多个类子目录;这将导致 BinPlace 生成文件的副本，并将其放入每个指定的位置。 有关完整详细信息，请参阅 [**放置文件语法**](place-file-syntax.md) 。 还可以使用-:D EST 类路径命令行参数来指定类子目录。

### <a name="span-idsymbol_file_destinationsspanspan-idsymbol_file_destinationsspansymbol-file-destinations"></a><span id="symbol_file_destinations"></span><span id="SYMBOL_FILE_DESTINATIONS"></span>符号文件目标

当可执行文件在 BinPlace 的命令行上列出并且在同一目录中存在关联的符号文件时，BinPlace 也会复制 (或更改符号文件) 。 在其中放置此符号文件的目录是通过连接三个目录创建的： *符号根目录*、 *类子目录* 和 *文件类型子目录*。

-   可以使用-s SymbolRoot 命令行参数指定符号根目录。 如果使用 **-a** 和 **-x** 开关，则被去除的符号文件将放在 *SymbolRoot* 目录下-在这种情况下，可以使用-n FullSymbolRoot 来指定完整符号文件的位置。

-   通常在位置文件中指定类子目录。 可以为一个文件指定多个类子目录;这将导致 BinPlace 生成文件的副本，并将其放入每个指定的位置。 有关完整详细信息，请参阅 [**放置文件语法**](place-file-syntax.md) 。 还可以使用-:D EST 类路径命令行参数来指定类子目录。 如果使用 **-y** 命令行开关，则不会将类子目录用于符号文件--目标目录只包含符号根目录和文件类型子目录。

-   文件类型子目录仅用于符号文件。 它由原始可执行文件的文件扩展名确定。 因此，与 .exe 文件相关联的符号文件将被放入 exe 子目录，与 Dll 关联的符号文件将放在 dll 子目录中，与驱动程序相关联的符号文件将放在 sys 子目录中。 此约定有助于避免文件名冲突，例如 myprogram.exe 和 myprogram.dll 可能具有名为 myprogram.exe 的符号文件，但这些符号文件将放在不同的子目录中。

此算法有一个例外。 如果不提供 **-s** 和 **-n** ，则完整的符号文件将放在与二进制文件相同的位置。

**注意**   如果在 BinPlace 的命令行中列出符号文件名，则 BinPlace 会将它与任何其他文件一起移动，而不会检查其内容。 若要使用 BinPlace 的符号文件操作方法，必须列出可执行文件的名称，而不是符号文件名。

 

 

 





