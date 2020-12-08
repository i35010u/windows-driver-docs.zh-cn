---
title: TraceView 的限制
description: TraceView 的限制
keywords:
- TraceView WDK，限制
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 77373f3f3bc53a64f25b8632db64dddf295671e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838099"
---
# <a name="traceview-limitations"></a>TraceView 的限制


本主题介绍了 TraceView 的限制。

## <a name="traceview-window-limitations"></a>TraceView 窗口限制

TraceView 窗口只能显示和控制使用该窗口启动的跟踪会话。 若要列出和控制系统上的所有跟踪会话，请使用 [TraceView 命令行接口](traceview-command-line-interface.md)。

退出 TraceView 时，它将停止所有正在运行的 (或使用 TraceView 启动的 *实时*) 跟踪会话。 若要启动独立于 TraceView 窗口运行的跟踪会话，请使用 TraceView 命令行接口。

可以使用 [TraceView 命令行接口](traceview-command-line-interface.md) 和其他软件跟踪工具（如 [Tracelog](tracelog.md)）来控制 TraceView 启动的跟踪会话。 但是，如果您使用这些其他工具来更改正在运行的跟踪会话的属性，TraceView 将停止跟踪会话，即使您更改了运行跟踪会话时可以更改的属性也是如此。 当你使用 TraceView 在跟踪会话) 重新启动 (或 *联接* 时，它将更新属性。

## <a name="traceview-command-line-limitations"></a>TraceView Command-Line 限制

当你在命令提示符窗口中提交 TraceView 命令时，TraceView 将打开一个新的命令提示符窗口以显示其输出。 不能取消这些其他窗口。

## <a name="etw-limitations"></a>ETW 限制

基于 Windows (ETW) 的事件跟踪的 TraceView 和其他跟踪工具只能为每个 WPP 或经典跟踪提供程序创建一个跟踪会话或显示一个跟踪日志。 如果您创建一个跟踪会话或使用已在另一个跟踪会话中启用的 WPP 提供程序显示跟踪日志，则它将在另一个会话中禁用。

## <a name="global-logger-trace-sessions"></a>全局记录器跟踪会话

TraceView 窗口没有启动 [全局记录器跟踪会话](global-logger-trace-session.md)的选项。 但是，您可以使用窗口来启动全局记录器跟踪会话，方法是输入全局记录器 [控件 guid](control-guid.md)e8908abc-aa84-11d2-9a93-00805f85d7c6，或将控件 guid 保存在 [控件 guid 文件](control-guid-file.md)中。 有关这些过程的详细信息，请参阅 [使用控件 GUID 创建跟踪会话](creating-a-trace-session-with-a-control-guid.md) 和 [使用 CTL 文件创建跟踪会话](creating-a-trace-session-with-a-ctl-file.md)。

还可以使用 [TraceView 命令行界面](traceview-command-line-interface.md) 启动全局记录器跟踪会话。 使用以下命令启动全局记录器跟踪会话。 此命令中的 "GlobalLogger" 一词区分大小写。

```dos
traceview -start GlobalLogger [parameters]
```

有关 TraceView 命令的详细信息，请参阅 [TraceView Control 命令](traceview-control-commands.md)。

## <a name="enabling-trace-providers"></a>启用跟踪提供程序

TraceView 会自动启用添加到跟踪会话的跟踪提供程序。 但是，在创建跟踪会话后，不能使用 TraceView 窗口为跟踪会话启用其他跟踪提供程序，也不能有选择地禁用已添加到跟踪会话的跟踪提供程序。

若要启用或禁用提供程序，请使用 **traceview** 命令。 有关此命令的详细信息，请参阅 [**TraceView Control 命令**](traceview-control-commands.md)。
