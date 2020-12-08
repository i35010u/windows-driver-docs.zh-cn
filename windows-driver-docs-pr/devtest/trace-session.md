---
title: 跟踪会话
description: 跟踪会话
keywords:
- 跟踪会话 WDK
- 跟踪会话 WDK，关于跟踪会话
- 会话 WDK 软件跟踪
- 专用跟踪会话 WDK
- 缓冲跟踪会话 WDK
- 实时跟踪会话 WDK
- 跟踪日志会话 WDK
- 用户模式跟踪会话 WDK
- 进程跟踪会话 WDK
- 保留跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 454692b615435bc38c5db4c12a8d3ee91334c61a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816899"
---
# <a name="trace-session"></a>跟踪会话


## <span id="ddk_trace_session_tools"></span><span id="DDK_TRACE_SESSION_TOOLS"></span>


*跟踪会话* 是 [跟踪提供程序](trace-provider.md)在其中生成跟踪消息的时间段。 系统为跟踪会话维护一组缓冲区，以存储跟踪消息，直到将跟踪消息传递 ( "刷新" ) 到 [跟踪日志](trace-log.md) 或 [跟踪使用者](trace-consumer.md)。

有三种基本类型的跟踪会话：跟踪日志会话、实时跟踪会话和缓冲跟踪会话。 单个跟踪会话可以是跟踪日志会话、实时跟踪会话或同时作为这两者。 缓冲跟踪会话是独占的。

此外，还存在专用跟踪会话和保留跟踪会话，如 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md) 和 [全局记录器跟踪会话](global-logger-trace-session.md)，可以作为日志会话或实时会话运行。 你可以使用标准工具来控制这些会话并显示生成的跟踪消息。

### <a name="span-idddk_trace_log_sessions_toolsspanspan-idddk_trace_log_sessions_toolsspantrace-log-sessions"></a><span id="ddk_trace_log_sessions_tools"></span><span id="DDK_TRACE_LOG_SESSIONS_TOOLS"></span>跟踪日志会话

在 *跟踪日志会话* 中，跟踪消息将从跟踪缓冲区写入到二进制格式的日志文件。 这是标准的默认跟踪会话类型。

### <a name="span-idddk_real_time_trace_sessions_toolsspanspan-idddk_real_time_trace_sessions_toolsspanreal-time-trace-sessions"></a><span id="ddk_real_time_trace_sessions_tools"></span><span id="DDK_REAL_TIME_TRACE_SESSIONS_TOOLS"></span>实时跟踪会话

在 *实时跟踪会话* 中，跟踪消息将直接传递给跟踪使用者（如 [TraceView](traceview.md) 或 [Tracefmt](tracefmt.md)），而不是发送到日志文件。

### <a name="span-idddk_buffered_trace_sessions_toolsspanspan-idddk_buffered_trace_sessions_toolsspanbuffered-trace-sessions"></a><span id="ddk_buffered_trace_sessions_tools"></span><span id="DDK_BUFFERED_TRACE_SESSIONS_TOOLS"></span>缓冲跟踪会话

在 *缓冲跟踪会话* 中，跟踪消息仍保留在跟踪缓冲区中;它们不会写入 [跟踪日志](trace-log.md) 或传递给 [跟踪使用者](trace-consumer.md)。 缓冲区的维护方式类似于循环文件。 当它已满时，最新的跟踪消息将覆盖缓冲区中最旧的跟踪消息。

只有 Windows Vista 和更高版本的 Windows 支持缓冲跟踪会话。

尽管软件跟踪通常会导致极少的开销，但缓冲跟踪会话的所有跟踪会话类型开销最小。 你可以跟踪较长的时间，然后，如果发生了一些有趣的事情，可以使用调试器来检查当前缓冲区内容，或者将当前缓冲区内容保存在跟踪日志中。

若要查看跟踪缓冲区中的跟踪消息，请使用 **！ wmitrace** 专用调试器扩展。 有关此扩展的信息，请参阅 *Windows 调试工具*。

若要将缓冲区内容刷新为 [跟踪日志](trace-log.md)，请使用 **tracelog-flush** 命令的 **-f** 参数。

若要启动缓冲跟踪会话，请使用 **tracelog** 命令的 **-缓冲** 参数。 有关详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)。

### <a name="span-idddk_private_trace_sessions_toolsspanspan-idddk_private_trace_sessions_toolsspanprivate-trace-sessions"></a><span id="ddk_private_trace_sessions_tools"></span><span id="DDK_PRIVATE_TRACE_SESSIONS_TOOLS"></span>专用跟踪会话

*专用跟踪会话* 是在用户模式下运行的跟踪会话，作为它跟踪的用户模式进程的一部分运行。  (内核中运行的标准跟踪会话。 ) 专用跟踪会话也称为 *用户模式跟踪* 会话或 *进程跟踪会话*。

您可以一次运行多个专用跟踪会话，但在每个进程中只能运行一个专用跟踪会话。

不能对专用跟踪会话执行实时跟踪。 跟踪消息必须写入日志。

专用跟踪会话中使用的缓冲区始终是可分页的。 不能为这些缓冲区指定分页或非分页内存。

不能将跟踪消息从专用跟踪会话发送到调试器。 WMI 跟踪扩展 (**！ wmitrace**) 不支持专用跟踪会话。

有关专用事件跟踪会话的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





