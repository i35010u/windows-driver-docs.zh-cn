---
title: TraceView 命令行接口
description: TraceView 命令行接口
keywords:
- TraceView WDK，命令行界面
- 命令 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afce14e73b54db86409ef2b78522e693bda6f44d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838103"
---
# <a name="traceview-command-line-interface"></a>TraceView 命令行接口

> [!IMPORTANT]
> TraceView 的命令行界面未包含独立工具中提供的所有最新更新。 建议改用 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)和 [Tracepdb](tracepdb.md) 。

使用 TraceView 命令行界面，可以在命令提示符窗口中控制 TraceView 功能。

命令行界面包含三个部分：

<span id="TraceView_Control_Commands"></span><span id="traceview_control_commands"></span><span id="TRACEVIEW_CONTROL_COMMANDS"></span>[**TraceView 控件命令**](traceview-control-commands.md)  
管理 TraceView 的 [跟踪控制器](trace-controller.md) 功能。 它类似于 [Tracelog](tracelog.md)。

<span id="TraceView_-process"></span><span id="traceview_-process"></span><span id="TRACEVIEW_-PROCESS"></span>[**TraceView-进程**](traceview--process.md)  
管理 TraceView 的 [跟踪使用者](trace-consumer.md) 功能。 它类似于 [Tracefmt](tracefmt.md)。

<span id="TraceView_-parsepdb"></span><span id="traceview_-parsepdb"></span><span id="TRACEVIEW_-PARSEPDB"></span>[**TraceView-parsepdb**](traceview--parsepdb.md)  
通过从[PDB 符号文件](pdb-symbol-files.md)中提取跟踪消息格式设置说明， [ () 文件创建跟踪消息格式](trace-message-format-file.md)。 它类似于 [Tracepdb](tracepdb.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

TraceView 窗口和 TraceView 命令行接口独立运行，不能互换使用。 您可以使用 TraceView 命令行界面来控制使用 TraceView 窗口启动的跟踪会话，但不能使用 TraceView 窗口来控制使用 TraceView 命令行界面启动的跟踪会话。

当你在命令提示符窗口中提交 TraceView 命令时，TraceView 会为其输出打开一个新的命令提示符窗口。 不能禁止显示其他窗口。
