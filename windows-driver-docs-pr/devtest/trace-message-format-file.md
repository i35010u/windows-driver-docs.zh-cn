---
title: 跟踪消息格式文件
description: 跟踪消息格式文件
ms.assetid: ac45475e-bf2d-4fa6-82fc-37ef8f4c0f6c
keywords:
- 跟踪消息格式文件 WDK
- TMF 文件 WDK
- 有关 TMF 文件 TMF 文件 WDK，
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdb426f98efcf82bf2a409c45d55d72854729a7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354741"
---
# <a name="trace-message-format-file"></a>跟踪消息格式文件


## <span id="ddk_trace_message_format_file_tools"></span><span id="DDK_TRACE_MESSAGE_FORMAT_FILE_TOOLS"></span>


*跟踪消息格式*(TMF) 文件是结构化的文本文件，其中包含用于分析的说明和格式设置的二进制跟踪消息[跟踪提供程序](trace-provider.md)生成。 格式设置的说明包含在跟踪提供程序的源代码中，会添加到由跟踪提供程序的 PDB 符号文件[WPP 预处理器](wpp-preprocessor.md)。

一些工具的日志，并显示格式化的跟踪消息需要 TMF 文件。 [Tracefmt](tracefmt.md)并[TraceView](traceview.md)，WDK 工具的格式并显示跟踪消息，可以使用 TMF 文件或者他们可以直接从 PDB 符号文件中提取的格式设置信息。

可以使用创建 TMF 文件[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)和包括 **-i**参数，它指示 Tracefmt 为 Tracedrv 创建 TMF 文件。 有关详细信息，请参阅[示例 9:创建 TMF 文件](https://docs.microsoft.com/windows-hardware/drivers/devtest/example-9--creating-a-tmf-file)。

如果你不具有 TMF 文件[跟踪提供程序](trace-provider.md)，使用[Tracepdb](tracepdb.md)。 Tracepdb PDB 符号文件中提取的格式设置的说明进行操作，并创建 TMF 文件来存储它们。 许多应用程序和驱动程序开发人员更喜欢传送 TMF 文件，而不是 PDB 符号文件。

TMF 文件的名称是[消息 GUID](message-guid.md)与该 TMF 文件相关联的消息。 ETW 使用消息的 GUID 将特定的跟踪消息与存放其格式设置的说明的 TMF 文件相关联。

TMF 文件包含以下数据：

-   从其提取 TMF 文件数据的 PDB 文件的名称。

-   [消息 GUID](message-guid.md)的跟踪中的消息源文件和源文件的名称。

-   为每个跟踪消息指定消息类型、 源代码文件名、 行号、 消息号、 消息定义字符串，跟踪标志名称和包含宏调用 C 函数的名称的条目。

-   其值显示在跟踪消息和与其相关联的内部类型名称的变量的列表。 变量表示由 %*n*消息定义字符串中的表示法。

**请注意**  TMF 文件保留供内部使用，并且其格式可能会更改的 Windows 不同版本之间。

 

 

 





