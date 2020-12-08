---
title: BinPlace 功能
description: BinPlace 功能
keywords:
- BinPlace WDK，功能
- 去除文件
- 拆分文件
- 移动文件 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2fd1f2277902e2ebda1d2f82e94d1d6b39fb931
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822565"
---
# <a name="binplace-capabilities"></a>BinPlace 功能


## <span id="ddk_binplace_capabilities_tools"></span><span id="DDK_BINPLACE_CAPABILITIES_TOOLS"></span>


BinPlace 主要执行三个操作：去除文件、拆分文件和移动文件。

### <a name="span-idstripping_filesspanspan-idstripping_filesspanstripping-files"></a><span id="stripping_files"></span><span id="STRIPPING_FILES"></span>去除文件

编译器和链接器创建的符号可以分为两个类别：公共符号和私有符号。 去除符号文件会删除私有符号信息，只留下公共符号信息。

有关详细信息，请参阅 [公共符号和私有符号](public-symbols-and-private-symbols.md)。

### <a name="span-idsplitting_filesspanspan-idsplitting_filesspansplitting-files"></a><span id="splitting_files"></span><span id="SPLITTING_FILES"></span>拆分文件

某些可执行文件包含符号。 BinPlace 可以将此排序文件拆分为两个文件：

-   没有可执行代码的符号文件

-   不带符号信息的可执行文件

有关详细信息，请参阅 [符号文件系统](symbol-file-systems.md)。

### <a name="span-idmoving_filesspanspan-idmoving_filesspanmoving-files"></a><span id="moving_files"></span><span id="MOVING_FILES"></span>移动文件

BinPlace 可移动文件。 当在可执行文件之外的任何文件上使用 BinPlace 时，它会将其移至目标目录树，而不会更改其内容。

当对可执行文件使用 BinPlace 时，如果在同一目录中存在关联的符号文件，则可执行文件和符号文件都将被移动。 如果选择了适当的 BinPlace 选项，也会发生去除或拆分。

对于大型项目，BinPlace 可用于将大量文件组织到适当的项目目录中。 如果要构建大量的二进制文件，并且要将这些文件的各个子集收集到不同的包中，BinPlace 可以管理此过程。

有关详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md)。

 

 





