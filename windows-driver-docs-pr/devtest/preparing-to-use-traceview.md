---
title: 准备使用 TraceView
description: 准备使用 TraceView
ms.assetid: 724e3c8a-7760-4e53-8d44-1927e5ad1efd
keywords:
- TraceView WDK，准备使用
- 文件 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff91a47ea2c8a4a31b791d1d2acf870ccbdb1f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327330"
---
# <a name="preparing-to-use-traceview"></a>准备使用 TraceView


## <span id="ddk_preparing_to_use_traceview_tools"></span><span id="DDK_PREPARING_TO_USE_TRACEVIEW_TOOLS"></span>


在使用 TraceView 之前，需要收集有关事件跟踪和有关的信息[跟踪提供程序](trace-provider.md)您正在跟踪的。 本主题介绍这些先决条件。

**请注意**  如果版本的 Windows 操作系统早于 Windows Vista 上运行 TraceView，必须将 Dbghelp.dll 文件复制到为 TraceView 可执行文件，TraceView.exe 相同的子目录。 

默认情况下，TraceView.exe 位于在工具\\ *&lt;平台&gt;* 子目录的 Windows Driver Kit (WDK) 中，其中 *&lt;平台&gt;* 是 i386、 amd64 或 ia64。 Dbghelp.dll 已安装，默认情况下，在\\bin\\x86 子目录。

 

### <a name="span-idunderstandeventtracingspanspan-idunderstandeventtracingspanunderstand-event-tracing"></a><span id="understand_event_tracing"></span><span id="UNDERSTAND_EVENT_TRACING"></span>了解事件跟踪

在使用 TraceView 之前，您应熟悉*事件跟踪*。 有关详细信息，请参阅[WPP 软件跟踪](wpp-software-tracing.md)和"[事件跟踪](https://go.microsoft.com/fwlink/p/?linkid=60384)"Microsoft Windows SDK 中的主题。

同时，检查 Tracedrv (Tracedrv.c) 使用 WPP 软件跟踪检测的示例驱动程序。 [Tracedrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)示例现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub 上的存储库。 生成 Tracedrv 驱动程序和其引擎，Tracectl (Tracectl.c)，然后使用驱动程序和引擎 TraceView 试验。

### <a name="span-idknowthetraceproviderspanspan-idknowthetraceproviderspanknow-the-trace-provider"></a><span id="know_the_trace_provider"></span><span id="KNOW_THE_TRACE_PROVIDER"></span>了解跟踪提供程序

您应熟悉[跟踪提供程序](trace-provider.md)您正在跟踪和类型的跟踪消息，它将生成。

TraceView 跟踪事件和跟踪消息以用户可读格式显示，但它不会将其解释或为消息提供任何信息或上下文。 若要了解消息和它们所指示的有关提供程序，您必须非常熟悉的提供程序的操作。

### <a name="span-idfindproviderfilesspanspan-idfindproviderfilesspanfind-provider-files"></a><span id="find_provider_files"></span><span id="FIND_PROVIDER_FILES"></span>查找提供程序的文件

若要查看来自跟踪提供程序的跟踪消息，将需要向 TraceView 提供以下位置之一：

-   位置[PDB 符号文件](pdb-symbol-files.md)提供程序

-   - 或 -

-   位置[控制 GUID (.ctl) 文件](control-guid-file.md)提供程序和位置[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)为其跟踪消息

[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)使用 WDK 中包含的 system.tmf 文件 (\\工具\\跟踪\\i386\)。

中介绍了这些文件和在 TraceView 中, 使用它们[NT 内核记录器跟踪会话的创建](creating-an-nt-kernel-logger-trace-session.md)。 创建跟踪会话时，将使用此信息。

 

 





