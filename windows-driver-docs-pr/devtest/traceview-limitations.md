---
title: TraceView 的限制
description: TraceView 的限制
ms.assetid: 946d7c69-7c6a-4bab-8fa5-fc21dcf85ddb
keywords:
- TraceView WDK 限制
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 852cc78489f444d45429c8176bccfabc45e07368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369623"
---
# <a name="traceview-limitations"></a>TraceView 的限制


本主题介绍 TraceView 的限制。

## <a name="traceview-window-limitations"></a>TraceView 窗口限制

TraceView 窗口可以显示和控制仅通过使用窗口中启动的跟踪会话。 列表和控制会话在系统上，使用的所有跟踪[TraceView 命令行界面](traceview-command-line-interface.md)。

当您退出 TraceView 时，它将停止所有正在运行 (或*实时*) 跟踪通过使用 TraceView 启动的会话。 若要开始运行的独立于 TraceView 窗口跟踪会话，请使用 TraceView 命令行接口。

可以使用[TraceView 命令行接口](traceview-command-line-interface.md)和其他软件跟踪工具，如[Tracelog](tracelog.md)，用于控制 TraceView 启动跟踪会话。 但是，如果使用其他工具来更改正在运行的跟踪会话的属性，TraceView 停止跟踪会话，即使更改跟踪会话正在运行时可以更改的属性。 当你使用 TraceView 重新启动 (或*联接*) 跟踪会话，它将更新的属性。

## <a name="traceview-command-line-limitations"></a>TraceView 命令行限制

当您提交 TraceView 命令在命令提示符窗口中的时，TraceView 将打开一个新的命令提示符窗口以显示其输出。 无法取消这些额外的窗口。

## <a name="etw-limitations"></a>ETW 限制

TraceView 和其他基于上事件跟踪 Windows (ETW) 的跟踪工具可以创建只有一个跟踪会话，或为每个 WPP 或经典跟踪提供程序显示一个跟踪日志。 如果在创建跟踪会话，或显示与 WPP 提供程序在另一个跟踪会话已启用跟踪日志，它将在其他会话中禁用它。

## <a name="global-logger-trace-sessions"></a>全局记录器跟踪会话

TraceView 窗口不具有用于启动选项[全局记录器跟踪会话](global-logger-trace-session.md)。 但是，可以使用窗口来首先全局记录器跟踪会话输入全局记录器[控制 GUID](control-guid.md)，e8908abc-aa84-11 d 2-9a93-00805f85d7c6，或者通过保存控件 GUID 在[控制 GUID 文件](control-guid-file.md). 有关这些过程的详细信息，请参阅[使用控件的 GUID 创建跟踪会话](creating-a-trace-session-with-a-control-guid.md)并[使用 CTL 文件创建跟踪会话](creating-a-trace-session-with-a-ctl-file.md)。

此外可以使用[TraceView 命令行界面](traceview-command-line-interface.md)启动全局记录器跟踪会话。 使用以下命令启动全局记录器跟踪会话。 在此命令中的"GlobalLogger"一词是区分大小写。

```dos
traceview -start GlobalLogger [parameters]
```

有关 TraceView 命令的详细信息，请参阅[TraceView 控制命令](traceview-control-commands.md)。

## <a name="enabling-trace-providers"></a>启用跟踪提供程序

TraceView 会自动启用的跟踪提供程序将添加到跟踪会话。 但是，在创建跟踪会话后，若要启用用于跟踪会话的其他跟踪提供程序，或有选择地禁用添加到跟踪会话的跟踪提供程序不能使用 TraceView 窗口。

若要启用或禁用提供程序，请使用**traceview-启用**命令。 有关此命令的详细信息，请参阅[ **TraceView 控制命令**](traceview-control-commands.md)。
