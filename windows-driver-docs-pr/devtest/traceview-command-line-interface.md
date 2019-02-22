---
title: TraceView 命令行接口
description: TraceView 命令行接口
ms.assetid: da38268f-ebdf-468c-95fe-500ba747047a
keywords:
- TraceView WDK，命令行接口
- WDK TraceView 命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2e74c971fc34d4d7da368ccf676d9d847b54c4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534549"
---
# <a name="traceview-command-line-interface"></a>TraceView 命令行接口

> [!IMPORTANT]
> TraceView 的命令行接口不包含所有最新的独立工具中提供更新。 建议你使用[Tracelog](tracelog.md)， [Tracefmt](tracefmt.md)，并[Tracepdb](tracepdb.md)相反。

TraceView 命令行界面，可控制从命令提示符窗口的 TraceView 功能。

命令行接口包含三个部分：

<span id="TraceView_Control_Commands"></span><span id="traceview_control_commands"></span><span id="TRACEVIEW_CONTROL_COMMANDS"></span>[**TraceView 控制命令**](traceview-control-commands.md)  
管理[跟踪控制器](trace-controller.md)TraceView 的功能。 它是类似于[Tracelog](tracelog.md)。

<span id="TraceView_-process"></span><span id="traceview_-process"></span><span id="TRACEVIEW_-PROCESS"></span>[**TraceView -process**](traceview--process.md)  
管理[跟踪使用者](trace-consumer.md)TraceView 的功能。 它是类似于[Tracefmt](tracefmt.md)。

<span id="TraceView_-parsepdb"></span><span id="traceview_-parsepdb"></span><span id="TRACEVIEW_-PARSEPDB"></span>[**TraceView -parsepdb**](traceview--parsepdb.md)  
创建[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)通过提取跟踪消息格式设置中的说明[PDB 符号文件](pdb-symbol-files.md)。 它是类似于[Tracepdb](tracepdb.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

TraceView 窗口和 TraceView 命令行接口将独立运行，并且不能互换使用。 可以使用 TraceView 命令行接口来控制通过使用 TraceView 窗口中，启动跟踪会话，但不是能使用以控制跟踪会话使用 TraceView 命令行界面启动 TraceView 窗口。

当提交 TraceView 命令在命令提示符窗口中的时，TraceView 将打开新的命令提示符窗口的其输出。 不能取消其他窗口。
