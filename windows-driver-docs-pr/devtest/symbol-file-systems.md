---
title: 符号文件系统
description: 符号文件系统
keywords:
- BinPlace WDK，符号文件系统
- 符号文件 WDK BinPlace
- 当前符号文件系统 WDK BinPlace
- 旧符号文件系统 WDK
- .pdf 文件
- pdf 符号文件 WDK BinPlace
- dbg 符号文件 WDK BinPlace
- .dbg 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8276c747156b6827e0378d69064c69fc51f32473
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791897"
---
# <a name="symbol-file-systems"></a>符号文件系统


## <span id="ddk_symbol_file_systems_tools"></span><span id="DDK_SYMBOL_FILE_SYSTEMS_TOOLS"></span>


共有两个常见符号文件系统。 在本文档中，这些将称为 *当前系统* 和 *旧系统*。

### <a name="span-idcurrent_symbol_file_systemspanspan-idcurrent_symbol_file_systemspancurrent-symbol-file-system"></a><span id="current_symbol_file_system"></span><span id="CURRENT_SYMBOL_FILE_SYSTEM"></span>当前符号文件系统

在当前系统中，始终有两个文件：可执行文件和 .pdb 文件。 .Pdb 文件包含所有符号。 可执行文件包含指向 .pdb 文件的指针。

如果 .pdb 符号文件包含 private 符号，则 BinPlace 可以将此信息包含在外，并生成一个去除的符号文件。 有关详细信息，请参阅 [公共符号和私有符号](public-symbols-and-private-symbols.md) 。

### <a name="span-idold_symbol_file_systemspanspan-idold_symbol_file_systemspanold-symbol-file-system"></a><span id="old_symbol_file_system"></span><span id="OLD_SYMBOL_FILE_SYSTEM"></span>旧符号文件系统

在旧系统中，可执行文件和符号文件可以通过两种不同的方式排列：

-   可执行文件和 .pdb 文件。 在这种排列中，大多数符号信息位于 .pdb 文件中。 符号信息的其余部分包括在可执行文件中。 可执行文件还包含指向 .pdb 文件的指针。

-   可执行文件、.pdb 文件和一个 dbg 文件。 .Pdb 文件与两个文件的排列方式相同：它包含大部分符号。 符号信息的其余部分在 dbg 文件中。 可执行文件中没有符号信息。 可执行文件包含指向 dbg 文件的指针，并且该文件包含指向 .pdb 文件的指针。

在旧的符号文件系统中，两文件排列和三文件排列都包含相同的可执行代码和相同的符号。 此程序可以运行，并可在两种排列中进行调试。 但是，这三个文件的排列会提高执行速度，因为可执行文件较小。

如果你的二进制文件是使用 arrangment 中的旧符号文件系统生成的，则 BinPlace 可以将其转换为三文件布局。 换句话说，BinPlace 可以将可执行文件 "拆分" 为一个无符号的可执行文件和一个新的 dbg 文件，其中包含可执行文件中的符号。

BinPlace 还可以从旧符号文件系统的文件中去除私有符号信息，但仅当它还将 (文件拆分为不同的文件时，才会将这些文件从两文件的排列方式更改为三个文件排列) 。 BinPlace 无法从旧符号文件系统中去除专用符号，并将其保留在两个文件中。 如果文件已处于三文件排列，则 BinPlace 不会执行任何去除;确实，如果可执行文件在 BinPlace 命令行上命名，它甚至不会移动符号文件。 有关详细信息，请参阅 [公共符号和私有符号](public-symbols-and-private-symbols.md) 。

 

 





