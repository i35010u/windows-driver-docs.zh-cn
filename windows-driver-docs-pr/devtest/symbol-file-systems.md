---
title: 符号文件系统
description: 符号文件系统
ms.assetid: 06f536e2-13d8-4727-9d34-a29a63eb01bc
keywords:
- BinPlace WDK，符号文件系统
- 符号文件 WDK BinPlace
- 当前符号文件系统 WDK BinPlace
- 旧的符号文件系统 WDK
- .pdf 文件
- pdf 符号文件必须 WDK BinPlace
- dbg 符号文件必须 WDK BinPlace
- .dbg 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2b789cb4f24ec4c92817348b5dcd591ae5927c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576948"
---
# <a name="symbol-file-systems"></a>符号文件系统


## <span id="ddk_symbol_file_systems_tools"></span><span id="DDK_SYMBOL_FILE_SYSTEMS_TOOLS"></span>


有两个常见的符号文件系统。 在本文档中，这些将称为*当前系统*并*旧系统*。

### <a name="span-idcurrentsymbolfilesystemspanspan-idcurrentsymbolfilesystemspancurrent-symbol-file-system"></a><span id="current_symbol_file_system"></span><span id="CURRENT_SYMBOL_FILE_SYSTEM"></span>当前符号文件系统

在当前系统中，始终有两个文件： 可执行文件和.pdb 文件。 .Pdb 文件包含所有符号。 可执行文件包含.pdb 文件的指针。

如果.pdb 符号文件包含私有符号，BinPlace 可以剥离出此信息并生成去除的符号文件。 请参阅[公共符号和私有符号](public-symbols-and-private-symbols.md)有关详细信息。

### <a name="span-idoldsymbolfilesystemspanspan-idoldsymbolfilesystemspanold-symbol-file-system"></a><span id="old_symbol_file_system"></span><span id="OLD_SYMBOL_FILE_SYSTEM"></span>旧的符号文件系统

在旧系统中，可执行文件和符号文件可以排列两个不同的方式：

-   可执行文件和.pdb 文件。 在这种方案，大多数符号信息是.pdb 文件中。 可执行文件中包含的符号信息的其余部分。 可执行文件还包含指向.pdb 文件的指针。

-   可执行文件、.pdb 文件和.dbg 文件。 .Pdb 文件是两个文件排列方式相同： 它包含的符号的大多数。 符号信息的其余部分是.dbg 文件中。 在可执行文件是没有对应符号信息。 可执行文件包含一个指向.dbg 文件，并且.dbg 文件包含.pdb 文件的指针。

在旧的符号文件系统中，两个文件排列方式和三个文件排列方式都包含相同的可执行代码和相同的符号。 该程序可以运行，并可以在任一种排列方式进行调试。 但是，三个文件排列方式执行速度，因为可执行文件的较小。

如果必须使用旧的符号文件系统中两个文件的排列方式放置生成的二进制文件，BinPlace 可以将其转换为三个文件排列方式。 换而言之，BinPlace 可以"拆分"的无符号的可执行文件将可执行文件和包含的符号的可执行文件中的新.dbg 文件。

BinPlace 可以还去除私有符号信息文件中旧的符号文件系统，但如果它将拆分文件 (即，仅当它从两个文件排列方式更改文件，对三个文件排列)。 BinPlace 不能将旧的符号文件系统中带文件去除私有符号，并将其留在两个文件排列方式。 如果文件已位于三个文件排列，BinPlace 将不执行任何去除; 和实际上，它不会甚至移动的符号文件如果 BinPlace 命令行上名为可执行文件。 请参阅[公共符号和私有符号](public-symbols-and-private-symbols.md)有关详细信息。

 

 





