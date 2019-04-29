---
title: BinPlace 功能
description: BinPlace 功能
ms.assetid: 2fd49ce3-8617-4c3e-bb86-8642343ca756
keywords:
- BinPlace WDK 功能
- 最小化文件
- 拆分文件
- 移动文件 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44deb199bc411e6015573d5c121f83ec1e1bfbfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324569"
---
# <a name="binplace-capabilities"></a>BinPlace 功能


## <span id="ddk_binplace_capabilities_tools"></span><span id="DDK_BINPLACE_CAPABILITIES_TOOLS"></span>


BinPlace 主要执行三个操作： 最小化文件，拆分文件，并将文件移动。

### <a name="span-idstrippingfilesspanspan-idstrippingfilesspanstripping-files"></a><span id="stripping_files"></span><span id="STRIPPING_FILES"></span>最小化文件

编译器和链接器创建的符号可以分为两类： 公共符号和私有符号。 最小化的符号文件删除私有符号信息，保留的公共符号信息。

有关详细信息，请参阅[公共符号和私有符号](public-symbols-and-private-symbols.md)。

### <a name="span-idsplittingfilesspanspan-idsplittingfilesspansplitting-files"></a><span id="splitting_files"></span><span id="SPLITTING_FILES"></span>拆分文件

某些可执行文件包含符号。 BinPlace 可以将此类的一个文件拆分到两个文件：

-   没有可执行代码的符号文件

-   可执行文件不包含符号信息

有关详细信息，请参阅[符号文件系统](symbol-file-systems.md)。

### <a name="span-idmovingfilesspanspan-idmovingfilesspanmoving-files"></a><span id="moving_files"></span><span id="MOVING_FILES"></span>移动文件

BinPlace 可以移动文件。 对可执行文件以外的任何文件使用 BinPlace 时，它将不会改变其内容将其移到其目标目录树中。

当 BinPlace 用于可执行文件，并在同一目录中没有关联的符号文件时，可执行文件和符号文件将同时移动。 如果已选择适当的 BinPlace 选项也会出现最小化或拆分。

对于大型项目，BinPlace 可以用于将大量文件组织到适当的项目目录。 如果要构建一组大型二进制文件，并且想要收集到不同的包的文件的各种子集 BinPlace 可以管理此过程。

有关详细信息，请参阅[BinPlace 目标目录](binplace-destination-directories.md)。

 

 





