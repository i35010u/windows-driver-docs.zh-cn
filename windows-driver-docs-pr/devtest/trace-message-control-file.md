---
title: 跟踪消息控制文件
description: 跟踪消息控制文件
ms.assetid: 4904a1d2-1314-49ad-bd57-ec976b18de13
keywords:
- 跟踪消息控制文件 WDK
- TMC 文件 WDK
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7809e05e07808a1fb948a13109fe678d815422c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380483"
---
# <a name="trace-message-control-file"></a>跟踪消息控制文件


**请注意**  在 Windows Vista 之前，此类型的文件已生成默认情况下[Tracepdb](tracepdb.md)。 相反，Tracepdb 工具现在会生成描述该二进制文件中的提供程序信息的 MOF (.mof) 文件。
除非您使用的[TraceView](traceview.md)，应忽略对这些 TMC 文件的引用。

 

一个*跟踪消息控件*(TMC) 文件是包含文本文件[控制 GUID](control-guid.md)每个[跟踪提供程序](trace-provider.md)在 PDB 文件中表示。 TMC 文件的名称是控件的跟踪提供程序后, 跟.tmc 文件扩展名的 GUID。

[Tracefmt](tracefmt.md)并[TraceView](traceview.md)为每个跟踪提供程序创建 TMC 文件，在创建时[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)PDB 文件中的格式设置操作说明。 [Tracepdb](tracepdb.md)使用时，还可以生成 TMC 文件 **-c**选项。

TMC 文件还包含以下信息：

-   PDB 文件的路径和文件名称。

-   日期和 PDB 文件的创建时间。

-   为每个跟踪提供程序的控件的 GUID。

-   [跟踪标志](trace-flags.md)由跟踪提供程序定义。

TraceView 使用 TMC 文件来查找每个提供程序的跟踪标志。 此文件可以用作控件的跟踪提供程序的 GUID 的快速参考。

 

 





