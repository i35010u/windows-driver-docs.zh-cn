---
title: 准备使用 TraceView
description: 准备使用 TraceView
keywords:
- TraceView WDK，准备使用
- 文件 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dfd55095d1685309cf2221a298e763ad05f17bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783309"
---
# <a name="preparing-to-use-traceview"></a>准备使用 TraceView


## <span id="ddk_preparing_to_use_traceview_tools"></span><span id="DDK_PREPARING_TO_USE_TRACEVIEW_TOOLS"></span>


使用 TraceView 之前，需要收集有关事件跟踪以及要跟踪的 [跟踪提供程序](trace-provider.md) 的信息。 本主题介绍这些先决条件。

**注意**   如果在 Windows Vista 之前的 Windows 操作系统版本上运行 TraceView，则必须将 Dbghelp.dll 文件复制到 TraceView 可执行文件所在的子目录中，TraceView.exe。 

默认情况下，TraceView.exe 位于 \\ Windows 驱动程序工具包的工具 *&lt; 平台 &gt;* 子目录中 (WDK) ，其中 *&lt; &gt; Platform* 为 i386、amd64 或 ia64。 默认情况下，在 \\ bin x86 子目录中安装 Dbghelp.dll \\ 。

 

### <a name="span-idunderstand_event_tracingspanspan-idunderstand_event_tracingspanunderstand-event-tracing"></a><span id="understand_event_tracing"></span><span id="UNDERSTAND_EVENT_TRACING"></span>了解事件跟踪

使用 TraceView 之前，应熟悉 *事件跟踪*。 有关详细信息，请参阅 [WPP Software 跟踪](wpp-software-tracing.md) 和 [Windows 事件跟踪](/windows-hardware/test/wpt/event-tracing-for-windows)。

另外，请检查 Tracedrv (Tracedrv) ，它是使用 WPP 软件跟踪进行检测的示例驱动程序。 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中提供了[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)示例。 构建 Tracedrv 驱动程序及其引擎，Tracectl (Tracectl) ，然后使用驱动程序和引擎试验 TraceView。

### <a name="span-idknow_the_trace_providerspanspan-idknow_the_trace_providerspanknow-the-trace-provider"></a><span id="know_the_trace_provider"></span><span id="KNOW_THE_TRACE_PROVIDER"></span>了解跟踪提供程序

你应该熟悉正在跟踪的 [跟踪提供程序](trace-provider.md) 以及它生成的跟踪消息的类型。

TraceView 以用户可读的格式显示跟踪事件和跟踪消息，但不会对其进行解释或为消息提供任何信息或上下文。 若要了解消息以及它们对提供程序的含义，你必须非常熟悉提供程序的操作。

### <a name="span-idfind_provider_filesspanspan-idfind_provider_filesspanfind-provider-files"></a><span id="find_provider_files"></span><span id="FIND_PROVIDER_FILES"></span>查找提供程序文件

若要查看跟踪提供程序中的跟踪消息，需要提供以下位置之一进行 TraceView：

-   提供程序的 [PDB 符号文件](pdb-symbol-files.md) 的位置

-   - 或 -

-   提供程序的[控件 GUID () 文件](control-guid-file.md)的位置，以及跟踪消息的跟踪[消息格式的位置 ( tmf) 文件](trace-message-format-file.md)

[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)使用 WDK (\\ 工具跟踪 i386 中包含的 tmf 文件 \\ \\ \) 。

这些文件及其在 TraceView 中的用法在 [创建 NT 内核记录器跟踪会话](creating-an-nt-kernel-logger-trace-session.md)中进行了介绍。 在创建跟踪会话时，将使用此信息。

 

