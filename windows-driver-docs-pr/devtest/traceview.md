---
title: TraceView
description: TraceView
ms.assetid: f64ddf90-56b8-4341-8d59-f4d7e3eeddaf
keywords:
- 跟踪 WDK，TraceView 软件
- 跟踪 WDK TraceView
- TraceView WDK
- 显示跟踪消息
- 跟踪消息显示 WDK
- 跟踪会话 WDK，TraceView
- 跟踪会话 WDK，控制
- 跟踪使用者 WDK
- 跟踪控制器 WDK
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b36bd02fc3054ee81e8f51ceb790ef88bc026b40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392690"
---
# <a name="traceview"></a>TraceView

## <span id="ddk_traceview_tools"></span><span id="DDK_TRACEVIEW_TOOLS"></span>

TraceView (TraceView.exe) 配置并控制[跟踪会话](trace-session.md)并显示格式化从实时跟踪会话的跟踪消息和[跟踪日志](trace-log.md)。

> [!IMPORTANT]
> TraceView 的命令行接口是已弃用和已过时。 应优先使用专用的 SDK 和 WDK 中包含的命令行工具：[Tracepdb](tracepdb.md)， [Tracelog](tracelog.md)，和[Tracefmt](tracefmt.md)。

是 TraceView[跟踪控制器](trace-controller.md)和一个[跟踪使用者](trace-consumer.md)。 TraceView 可用于启用、 配置、 启动、 更新和停止跟踪会话;若要显示实时或记录的跟踪消息;若要将合并来自不同的提供程序在单个显示屏; 跟踪消息若要筛选显示的跟踪消息;并将跟踪消息转换为文本格式。

工具中位于 TraceView\\&lt;*平台*&gt;子目录的 Windows Driver Kit (WDK) 中，其中&lt;*平台*&gt;表示正在跟踪会话，例如，x86、 x64、 或 arm64 的平台。

本部分介绍 TraceView 随附在 Windows 10 Fall Creators Update (1709) WDK 和更高版本的版本。 早期版本的 Traceview 可能没有很多此处所述的功能。

> [!NOTE]
> TraceView 在 Microsoft Windows 7 和更高版本的 Windows 上运行。

* [TraceView 概述](traceview-overview.md)

[使用 TraceView](using-traceview.md)
