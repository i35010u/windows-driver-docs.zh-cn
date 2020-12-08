---
title: Tracepdb 概述
description: Tracepdb 概述
keywords:
- Tracepdb WDK
- 跟踪消息控制文件 WDK
- TMC 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2be036b947a5bb2be46b863122b332fbb74b7d79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838115"
---
# <a name="tracepdb-overview"></a>Tracepdb 概述


[跟踪提供](trace-provider.md)程序（如用户模式应用程序和内核模式驱动程序）将其跟踪消息存储为二进制格式，以便提高效率。 若要读取跟踪消息，您必须为跟踪提供程序代码中的每个跟踪消息应用指定的格式设置指令。

[WPP 预处理器](wpp-preprocessor.md)从跟踪提供程序的代码中提取格式说明，并将其添加到跟踪提供程序的[PDB 符号文件](pdb-symbol-files.md)中。

Tracepdb 从跟踪提供程序的 PDB 符号文件的完全或私有版本中提取格式说明， (从公共符号文件中去除跟踪格式设置指令。 ) 并为源代码中的每个跟踪提供程序创建[跟踪消息格式 (.) tmf。](trace-message-format-file.md) TMF 文件是文本文件，仅包含提供程序的跟踪消息的格式说明。

用可读格式（例如 [TraceView](traceview.md) 和 [Tracefmt](tracefmt.md)）显示跟踪消息的工具使用 TMF 文件来分析和格式化跟踪消息。 此外，你还可以将 TMF 文件分发给用户，而不是分发私有符号文件。

Tracepdb 创建一个 MOF ( mof) 文件，其中包含 PDB 文件中表示的每个跟踪提供程序的控件 GUID 和跟踪级别。 MOF 文件的名称为跟踪提供程序的模块名称。

如果使用 **-c** 选项，Tracepdb 还可以为源代码中的每个跟踪提供程序创建 [跟踪消息控制 ( tmc) 文件](trace-message-control-file.md)。 TMC 文件包含 PDB 文件中表示的每个跟踪提供程序的 [控件 GUID](control-guid.md) 和跟踪级别。 TMC 文件的名称为 [跟踪提供程序](trace-provider.md)的控件 GUID。 如果使用的是不带 PDB 文件的 Traceview，则应仅关心 TMC 文件。

Tracepdb 的唯一功能是创建 TMF 文件。 但是，其他工具（如 [BinPlace](binplace.md)、TraceView 和 Tracefmt）除了创建其他功能外，还会创建 TMF 文件。 使用 Tracepdb 等效于使用 **binplace-： tmf** 命令、 **traceview-parsepdb** 命令和 **tracefmt-i** 命令。

在 Windows Vista 之前的系统上，Tracepdb 需要 mspdb70.dll 和 msvcr70.dll。 如果这些文件与 Tracepdb.exe 文件不在同一目录中，请在使用 Tracepdb 之前移动它们。

在 windows Vista 之前的系统上，必须从 windows 驱动程序工具包的 "bin 平台子目录" 中复制 Dbghelp.dll 文件 \\ &lt; *Platform* &gt; (WDK)  (其中 &lt; *平台* &gt; 是 x86、amd64 或 ia64) 到 Tracefmt.exe 所在的目录中。

有关事件跟踪的详细信息，请参阅 Windows SDK 文档。 有关在内核模式驱动程序和用户模式应用程序中使用事件跟踪的信息，请参阅 [WPP 软件跟踪](wpp-software-tracing.md)。

 

 





