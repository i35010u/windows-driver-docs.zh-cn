---
title: PDB 符号文件
description: PDB 符号文件
ms.assetid: 077784d9-06be-450c-bdd5-02321305df1b
keywords:
- 程序数据库符号文件 WDK
- WDK 的 PDB 符号文件
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482df3ee811b54185e4e48f9b9df6fc064ad0880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356327"
---
# <a name="pdb-symbol-files"></a>PDB 符号文件


## <span id="ddk_pdb_symbol_files_tools"></span><span id="DDK_PDB_SYMBOL_FILES_TOOLS"></span>


程序数据库 (PDB) 符号文件[跟踪提供程序](trace-provider.md)，如应用程序或驱动程序，包括有关设置跟踪消息格式，以便它们可以出现在显示模式中的可读的说明。

跟踪消息格式说明是跟踪提供程序源代码的一部分。 [WPP 预处理器](wpp-preprocessor.md)将其提取的代码并将它们添加到跟踪提供程序的 PDB 符号文件。

编译器在编译的跟踪提供程序 （已选中） 的调试版本生成 PDB 文件。 生成进程默认情况下使用时都创建 PDB 文件[BinPlace](binplace.md)构建跟踪提供程序。

[跟踪使用者](trace-consumer.md)在 WDK [TraceView](traceview.md)并[Tracefmt](tracefmt.md)，可以提取跟踪消息格式设置信息直接从 PDB 文件或 TMF 文件。 其他需要 TMF 文件。 [Tracepdb](tracepdb.md)将 PDB 文件作为输入，将提取的格式设置信息和创建 TMF 文件作为输出。

不要使用其他跟踪使用者，如 Tracerpt，Windows，在包含的工具，PDB 文件或 TMF 文件。 相反，它们使用的信息在托管对象格式 (MOF) 文件中设置跟踪事件的格式。 这些工具不能设置跟踪消息的格式。

 

 





