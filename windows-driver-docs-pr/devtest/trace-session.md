---
title: 跟踪会话
description: 跟踪会话
ms.assetid: 50a8cc64-5127-4abe-a6a8-514ca5db63ab
keywords:
- 跟踪会话 WDK
- 有关跟踪会话的跟踪会话 WDK，
- 会话 WDK 软件跟踪
- 专用跟踪会话 WDK
- 缓冲的跟踪会话 WDK
- 实时跟踪会话 WDK
- 跟踪日志会话 WDK
- 用户模式跟踪会话 WDK
- 处理跟踪会话 WDK
- 保留的跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8007a394639abeb3d5382ab7aaa13222958d62eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392694"
---
# <a name="trace-session"></a>跟踪会话


## <span id="ddk_trace_session_tools"></span><span id="DDK_TRACE_SESSION_TOOLS"></span>


一个*跟踪会话*是一段时间内这[跟踪提供程序](trace-provider.md)生成跟踪消息。 系统会向维护一组跟踪会话来存储跟踪消息，直到被传递 （"刷新"） 的缓冲区[跟踪日志](trace-log.md)或[跟踪使用者](trace-consumer.md)。

有三种基本类型的跟踪会话： 跟踪日志会话、 实时跟踪会话和缓存的跟踪会话。 单个跟踪会话可以是一个跟踪日志会话、 实时跟踪会话，或两者。 缓冲的跟踪会话是互斥的。

此外，有专用的跟踪会话和保留的跟踪会话，如[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)并[全局记录器跟踪会话](global-logger-trace-session.md)，可以是日志会话以运行或实时会话。 标准工具可用于控制这些会话，并显示生成的跟踪消息。

### <a name="span-idddktracelogsessionstoolsspanspan-idddktracelogsessionstoolsspantrace-log-sessions"></a><span id="ddk_trace_log_sessions_tools"></span><span id="DDK_TRACE_LOG_SESSIONS_TOOLS"></span>跟踪日志会话

在中*跟踪日志会话*，跟踪消息将从跟踪缓冲区写入到二进制格式中的日志文件。 这是跟踪会话的标准，默认类型。

### <a name="span-idddkrealtimetracesessionstoolsspanspan-idddkrealtimetracesessionstoolsspanreal-time-trace-sessions"></a><span id="ddk_real_time_trace_sessions_tools"></span><span id="DDK_REAL_TIME_TRACE_SESSIONS_TOOLS"></span>实时跟踪会话

在中*实时跟踪会话*，跟踪消息会直接传递到跟踪使用者，如[TraceView](traceview.md)或[Tracefmt](tracefmt.md)、 而不是或，除了，发送发送到日志文件。

### <a name="span-idddkbufferedtracesessionstoolsspanspan-idddkbufferedtracesessionstoolsspanbuffered-trace-sessions"></a><span id="ddk_buffered_trace_sessions_tools"></span><span id="DDK_BUFFERED_TRACE_SESSIONS_TOOLS"></span>缓冲的跟踪会话

在中*缓冲跟踪会话*，跟踪消息保持跟踪缓冲区中; 它们不会写入到[跟踪日志](trace-log.md)或传递到[跟踪使用者](trace-consumer.md)。 缓冲区被维护等循环文件。 如果它已满，最新的跟踪消息将覆盖缓冲区中最旧的跟踪消息。

仅在 Windows Vista 和更高版本的 Windows 上支持缓冲的跟踪会话。

虽然一般情况下，跟踪软件，使极少的开销，但缓存的跟踪会话的开销最少的所有跟踪会话类型。 你可以跟踪长时间，然后，如果出现一些有趣的事情，您可以使用调试器来检查当前缓冲区的内容，或将当前缓冲区的内容保存在跟踪日志。

若要查看跟踪缓冲区中的跟踪消息，请使用 **！ wmitrace**专用调试器扩展。 有关此扩展的信息，请参阅*有关 Windows 调试工具*。

若要刷新内容到缓冲区[跟踪日志](trace-log.md)，使用 **-f**参数**tracelog-刷新**命令。

若要启动缓存的跟踪会话，请使用 **-缓冲**的参数**tracelog-启动**命令。 有关详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

### <a name="span-idddkprivatetracesessionstoolsspanspan-idddkprivatetracesessionstoolsspanprivate-trace-sessions"></a><span id="ddk_private_trace_sessions_tools"></span><span id="DDK_PRIVATE_TRACE_SESSIONS_TOOLS"></span>专用跟踪会话

一个*专用跟踪会话*是它跟踪的用户模式进程的一部分在用户模式下运行的跟踪会话。 （标准跟踪会话的内核中运行。）专用跟踪会话也被称为*用户模式跟踪会话*或*处理跟踪会话*。

你可以一次运行多个专用跟踪会话，但你可以在每个进程运行只有一个专用的跟踪会话。

不能执行专用跟踪会话的实时的跟踪。 跟踪消息必须写入日志。

在专用跟踪会话中使用的缓冲区始终是可分页。 不能指定分页或非分页内存用于这些缓冲区。

不能将从专用跟踪会话的跟踪消息都发送到调试器中。 WMI 跟踪扩展 (**！ wmitrace**) 不支持专用跟踪会话。

有关专用事件跟踪会话的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





