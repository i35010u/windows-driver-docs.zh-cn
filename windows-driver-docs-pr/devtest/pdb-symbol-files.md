---
title: PDB 符号文件
description: PDB 符号文件
keywords:
- 程序数据库符号文件 WDK
- PDB 符号文件 WDK
- 符号文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ee6998a596bc5a4caa9bbfb896a94dda0aa81e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838995"
---
# <a name="pdb-symbol-files"></a>PDB 符号文件


## <span id="ddk_pdb_symbol_files_tools"></span><span id="DDK_PDB_SYMBOL_FILES_TOOLS"></span>


[跟踪提供](trace-provider.md)程序的程序数据库 (PDB) 符号文件（如应用程序或驱动程序）包含用于设置跟踪消息格式的说明，以便在可读的显示中显示这些消息。

跟踪消息格式说明是跟踪提供程序源代码的一部分。 [WPP 预处理器](wpp-preprocessor.md)从代码中提取它们，并将它们添加到跟踪提供程序的 PDB 符号文件中。

编译调试 (检查跟踪提供程序的) 版本时，编译器将生成 PDB 文件。 默认情况下，在使用 [BinPlace](binplace.md) 生成跟踪提供程序时，生成过程会创建 PDB 文件。

WDK、 [TraceView](traceview.md)和[Tracefmt](tracefmt.md)中的[跟踪使用者](trace-consumer.md)可以直接从 PDB 文件或 TMF 文件中提取跟踪消息格式信息。 其他人需要 TMF 文件。 [Tracepdb](tracepdb.md) 采用 PDB 文件作为输入，提取格式设置信息，并创建 TMF 文件作为输出。

其他跟踪使用者（如 Tracerpt）是 Windows 中包含的工具，不使用 PDB 文件或 TMF 文件。 相反，它们使用托管对象格式 (MOF) 文件中的信息来格式化跟踪事件。 这些工具无法格式化跟踪消息。

 

 





