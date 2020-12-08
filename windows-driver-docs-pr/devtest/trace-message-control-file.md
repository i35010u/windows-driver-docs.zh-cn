---
title: 跟踪消息控制文件
description: 跟踪消息控制文件
keywords:
- 跟踪消息控制文件 WDK
- TMC 文件 WDK
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07f39f238c932e7ebabe089268e4487b985de831
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830131"
---
# <a name="trace-message-control-file"></a>跟踪消息控制文件


**注意**  在 Windows Vista 之前， [Tracepdb](tracepdb.md)默认生成此类文件。 相反，Tracepdb 工具现在会生成 MOF ( mof) 文件，用于描述二进制文件中的提供程序信息。
除非使用 [TraceView](traceview.md)，否则应忽略对这些 TMC 文件的引用。

 

*跟踪消息控件* (TMC) 文件是一个文本文件，该文件包含 PDB 文件中表示的每个 [跟踪提供程序](trace-provider.md)的 [控件 GUID](control-guid.md) 。 TMC 文件的名称为跟踪提供程序的控件 GUID，后跟 TMC 文件扩展名。

[Tracefmt](tracefmt.md) 和 [TraceView](traceview.md) 创建跟踪消息格式时，将为每个跟踪提供程序创建一个 TMC 文件 [ (. tmf) 文件](trace-message-format-file.md) 中的格式说明。 使用 **-c** 选项时， [Tracepdb](tracepdb.md)还可以生成 TMC 文件。

TMC 文件还包含以下信息：

-   PDB 文件的路径和文件名。

-   创建 PDB 文件的日期和时间。

-   每个跟踪提供程序的控件 GUID。

-   跟踪提供程序定义的 [跟踪标志](trace-flags.md) 。

TraceView 使用 TMC 文件查找每个提供程序的跟踪标志。 您可以使用此文件作为跟踪提供程序的控件 GUID 的快速参考。

 

 





