---
title: 跟踪消息格式文件
description: 跟踪消息格式文件
ms.assetid: ac45475e-bf2d-4fa6-82fc-37ef8f4c0f6c
keywords:
- 跟踪消息格式化文件 WDK
- TMF 文件 WDK
- TMF 文件 WDK，关于 TMF 文件
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e4c2d39f4a598f3c3fbc5137b83e8135b0892a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381949"
---
# <a name="trace-message-format-file"></a>跟踪消息格式文件


## <span id="ddk_trace_message_format_file_tools"></span><span id="DDK_TRACE_MESSAGE_FORMAT_FILE_TOOLS"></span>


*跟踪消息格式* (TMF) 文件是结构化文本文件，其中包含用于分析和格式化[跟踪提供程序](trace-provider.md)生成的二进制跟踪消息的说明。 格式设置指令包含在跟踪提供程序的源代码中，并由 [WPP 预处理器](wpp-preprocessor.md)添加到跟踪提供程序的 PDB 符号文件中。

某些用于记录和显示格式化跟踪消息的工具需要 TMF 文件。 [Tracefmt](tracefmt.md) 和 [TraceView](traceview.md)是格式化和显示跟踪消息的 WDK 工具，可以使用 TMF 文件，也可以直接从 PDB 符号文件中提取格式设置信息。

可以通过使用 [Tracefmt](./tracefmt.md) 创建 TMF 文件，并包括 **-i** 参数，该参数指示 TRACEFMT 创建 Tracedrv 的 TMF 文件。 有关详细信息，请参阅 [示例9：创建 TMF 文件](./example-9--creating-a-tmf-file.md)。

如果没有 [跟踪提供程序](trace-provider.md)的 TMF 文件，请使用 [Tracepdb](tracepdb.md)。 Tracepdb 提取 PDB 符号文件中的格式设置指令，并创建 TMF 文件来存储它们。 许多应用程序和驱动程序开发人员都倾向于传送 TMF 文件，而不是 PDB 符号文件。

TMF 文件的名称为与该 TMF 文件关联的消息的 [消息 GUID](message-guid.md) 。 ETW 使用消息 GUID 将特定跟踪消息与保存其格式设置说明的 TMF 文件相关联。

TMF 文件包含以下数据：

-   从中提取 TMF 文件数据的 PDB 文件的名称。

-   源文件中跟踪消息的 [消息 GUID](message-guid.md) 和源文件名。

-   对于每个跟踪消息，指定消息类型、源代码文件名称、行号、消息号、消息定义字符串、跟踪标志名称以及包含宏调用的 C 函数的名称的项。

-   其值出现在跟踪消息及其关联的内部类型名称中的变量的列表。 变量由消息定义字符串中的%*n* 表示法表示。

**注意**   TMF 文件保留供内部使用，其格式在不同的 Windows 版本之间可能会更改。

 

 

