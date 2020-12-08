---
title: TraceView
description: TraceView
keywords:
- 软件跟踪 WDK，TraceView
- 跟踪 WDK，TraceView
- TraceView WDK
- 显示跟踪消息
- 显示 WDK 的跟踪消息
- 跟踪会话 WDK，TraceView
- 跟踪会话 WDK，控制
- 跟踪使用者 WDK
- 跟踪控制器 WDK
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4eb5ee691c99f4d66bfee3294a8d1043b5146c1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838095"
---
# <a name="traceview"></a>TraceView

## <span id="ddk_traceview_tools"></span><span id="DDK_TRACEVIEW_TOOLS"></span>

TraceView ( # A0) 配置和控制 [跟踪会话](trace-session.md) ，并显示实时跟踪会话和 [跟踪日志](trace-log.md)中的格式化跟踪消息。

> [!IMPORTANT]
> TraceView 的命令行接口已弃用并过时。 你应首选 SDK 和 WDK 中包含的专用命令行工具：  [Tracepdb](tracepdb.md)、 [Tracelog](tracelog.md)和 [Tracefmt](tracefmt.md)。

TraceView 是 [跟踪控制器](trace-controller.md) 和 [跟踪使用者](trace-consumer.md)。 你可以使用 TraceView 来启用、配置、启动、更新和停止跟踪会话;显示实时跟踪消息或记录跟踪消息;若要在单个显示器中合并来自不同提供程序的跟踪消息，则为;筛选跟踪消息显示;和将跟踪消息转换为文本格式。

TraceView 位于 \\ &lt; *Platform* &gt; Windows 驱动程序工具包 (WDK) 的工具平台子目录中，其中 &lt; *platform* &gt; 表示正在运行跟踪会话的平台，例如 x86、x64 或 arm64。

本部分介绍 Windows 10 秋季创建者更新 (1709) WDK 和更高版本中随附的 TraceView 版本。 更早版本的 Traceview 可能缺少此处所述的许多功能。

> [!NOTE]
> TraceView 在 Microsoft Windows 7 和更高版本的 Windows 上运行。

* [TraceView 概述](traceview-overview.md)

[使用 TraceView](using-traceview.md)
