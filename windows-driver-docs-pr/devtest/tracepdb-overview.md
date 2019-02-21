---
title: Tracepdb 概述
description: Tracepdb 概述
ms.assetid: ec13726f-65e6-4aef-b2b1-a4bddcd73a37
keywords:
- Tracepdb WDK
- 跟踪消息控制文件 WDK
- TMC 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cd4d57a3e28d7f47f05d866f3ad4c5d43c661c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524385"
---
# <a name="tracepdb-overview"></a>Tracepdb 概述


[跟踪提供程序](trace-provider.md)，例如用户模式应用程序和内核模式驱动程序，以提高效率的二进制格式存储其跟踪消息。 若要阅读的跟踪消息，你必须应用为每条跟踪消息跟踪提供程序代码中指定的格式设置的说明进行操作。

[WPP 预处理器](wpp-preprocessor.md)从跟踪提供程序的代码中提取的格式设置的说明进行操作，并将它们添加到[PDB 符号文件](pdb-symbol-files.md)跟踪提供程序。

Tracepdb 跟踪提供程序 （跟踪格式设置的说明从公共符号文件。 去除） 从 PDB 符号文件的完整或专用版本提取的格式设置的说明进行操作，并创建[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)每个跟踪提供程序的源代码中。 TMF 文件是包含只有在提供程序的跟踪消息的格式设置说明的文本文件。

可读格式，如显示跟踪消息的工具[TraceView](traceview.md)并[Tracefmt](tracefmt.md)，TMF 文件用于分析和格式化跟踪消息。 另外，还可以分配给用户，而不是分发私有符号文件 TMF 文件。

Tracepdb 创建 MOF (.mof) 文件，其中包含控件的 GUID 和 PDB 文件中表示的跟踪级别的每个跟踪提供程序。 MOF 文件的名称是跟踪提供程序的模块名称。

此外可以创建 Tracepdb[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)如果你使用的源代码中每个跟踪提供程序 **-c**选项。 TMC 文件包含[控制 GUID](control-guid.md)和 PDB 文件中表示每个跟踪提供程序的跟踪级别。 TMC 文件的名称是 GUID 的控件的[跟踪提供程序](trace-provider.md)。 您应只关心 TMC 文件如果你将不使用 PDB 文件使用 Traceview。

Tracepdb 的唯一函数是创建 TMF 文件。 但是，其他工具，如[BinPlace](binplace.md)，TraceView 和 Tracefmt，创建 TMF 文件，除了其他功能... 使用 Tracepdb 相当于使用**binplace-: tmf**命令， **traceview parsepdb**命令，并且**tracefmt-i**命令。

在 Windows Vista 之前的系统，Tracepdb 都需要 mspdb70.dll 和 msvcr70.dll。 如果这些文件不在 Tracepdb.exe 文件所在的同一目录中，将使用 Tracepdb 之前将它们移。

在系统上 Windows Vista 之前，必须从 bin 将 Dbghelp.dll 文件\\&lt;*平台*&gt;子目录的 Windows Driver Kit (WDK) (其中&lt; *平台*&gt;是任一 x86、amd64 或 ia64) 到 Tracefmt.exe 所在的目录。

有关事件跟踪的详细信息，请参阅 Windows SDK 文档。 有关使用内核模式驱动程序和用户模式应用程序中的事件跟踪的信息，请参阅[WPP 软件跟踪](wpp-software-tracing.md)。

 

 





