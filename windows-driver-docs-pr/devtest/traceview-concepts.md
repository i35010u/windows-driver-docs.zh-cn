---
title: TraceView 的概念
description: TraceView 的概念
ms.assetid: 4fab2b23-8f7b-407b-b944-41ac8caf1a75
keywords:
- TraceView WDK，术语
- 跟踪会话 WDK，组
- 分组跟踪会话
- 工作区 WDK TraceView，关于工作区
- 跟踪会话 WDK，工作区
- 跟踪提供程序 WDK
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
- TMF 文件 WDK，搜索路径
- 搜索路径 WDK 软件跟踪
- TMF 文件 WDK，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9dd4490083696771d9f529c3cbc96728163c28d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383077"
---
# <a name="traceview-concepts"></a>TraceView 的概念

## <span id="ddk_traceview_concepts_tools"></span><span id="DDK_TRACEVIEW_CONCEPTS_TOOLS"></span>

本主题介绍 TraceView 中使用的概念。

有关 WDK 中的跟踪工具所共有的概念的信息，请参阅 [跟踪工具概念](tracing-tool-concepts.md)。

### <a name="span-idtrace_session_groupspanspan-idtrace_session_groupspanspan-idtrace_session_groupspantrace-session-group"></a><span id="Trace_Session_Group"></span><span id="trace_session_group"></span><span id="TRACE_SESSION_GROUP"></span>跟踪会话组

TraceView 使你可以将 [跟踪日志](trace-log.md) 显示或实时跟踪会话合并为 *跟踪会话组* ，并将其作为单个会话进行管理。 当跟踪日志或会话位于同一跟踪会话组中时，其消息会合并到一个 [跟踪消息列表](trace-message-lists.md)中。

默认情况下，每个跟踪会话都是跟踪会话组的成员，该组仅由该跟踪会话组成。

有关创建跟踪会话组的信息，请参阅对 [跟踪会话进行分组](grouping-trace-sessions.md)。

### <a name="span-idworkspacespanspan-idworkspacespanspan-idworkspacespanworkspace"></a><span id="Workspace"></span><span id="workspace"></span><span id="WORKSPACE"></span>空间

在 TraceView 中， *工作区* 是一组跟踪会话属性和跟踪日志显示属性，可以保存和重复使用。 使用工作区，可以快速显示经常使用的日志或启动仔细配置的跟踪会话。

工作区包括：

- 跟踪会话的所有属性，包括缓冲区、标志和级别，以及跟踪日志的位置

- [程序数据库 (PDB) 符号文件](pdb-symbol-files.md)、[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)或 TMF 搜索路径的位置

- TraceView 列表文件和摘要文件的路径和文件名

- [筛选器](filtering-trace-messages.md)

当你为实时跟踪会话打开工作区时，TraceView 将使用保存的属性和配置设置启动一个新的跟踪会话。 为跟踪日志显示打开工作区时，该日志的显示方式与配置日志的方式完全相同。

有关详细信息，请参阅 [使用 TraceView 工作区](using-traceview-workspaces.md)。

### <a name="span-idspecifying_trace_providersspanspan-idspecifying_trace_providersspanspan-idspecifying_trace_providersspanspecifying-trace-providers"></a><span id="Specifying_Trace_Providers"></span><span id="specifying_trace_providers"></span><span id="SPECIFYING_TRACE_PROVIDERS"></span>指定跟踪提供程序

若要创建跟踪会话，必须标识跟踪提供程序，并找到提供程序生成的二进制跟踪消息的格式说明。 可以通过以下方式之一执行此操作：

- 找到行提供程序所对应的源代码的可执行二进制文件。 TraceView 可以提取启用和格式化 [TRACELOGGING](/windows/desktop/tracelogging/trace-logging-portal) ETW 事件所需的所有信息。 它还将尝试查找 [PDB 符号文件](pdb-symbol-files.md) 以启用任何 [WPP 软件跟踪](wpp-software-tracing.md) 提供程序。

- 找到包含[WPP 软件跟踪](wpp-software-tracing.md)提供程序的源代码的[PDB 符号文件](pdb-symbol-files.md)。 TraceView 可以从 PDB 文件中提取标识提供程序所需的所有信息，并设置跟踪消息的格式。

- 找到该提供程序的 [控件 GUID ( ctl) 文件](control-guid-file.md) ，并指定 [TMF 文件](trace-message-format-file.md) 或 TMF 文件所在目录的路径。

- 输入提供程序的 [控件 GUID](control-guid.md) ，并指定 TMF 文件或存储 TMF 文件的目录的路径。

    如果输入的提供程序名称前面有一个星号 (例如 ```*SampleProvider```) ，TraceView 将使用标准算法自动将该名称转换为 GUID。 并非所有提供程序都遵循此标准，但许多提供程序（如使用编写的提供程序） [。NET 的 EventSource](/dotnet/api/system.diagnostics.tracing.eventsource?view=netframework-4.8)，do。

- 从 TraceView 汇编的列表中选择一个 [已注册的提供程序](registered-provider.md) ，并指定 TMF 文件或存储 TMF 文件的目录的路径。

- 选择一个 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，然后选择一个或多个要跟踪的操作系统事件。

### <a name="span-idset_tmf_search_path_and_select_tmf_files_optionsspanspan-idset_tmf_search_path_and_select_tmf_files_optionsspanspan-idset_tmf_search_path_and_select_tmf_files_optionsspanset-tmf-search-path-and-select-tmf-files-options"></a><span id="Set_TMF_Search_Path_and_Select_TMF_Files_Options"></span><span id="set_tmf_search_path_and_select_tmf_files_options"></span><span id="SET_TMF_SEARCH_PATH_AND_SELECT_TMF_FILES_OPTIONS"></span>设置 TMF 搜索路径并选择 TMF 文件选项

启用 WPP 提供程序时，除非您有提供程序的 [PDB 符号文件](pdb-symbol-files.md) ，否则您必须指定 TraceView 可以在其中找到 TMF 文件的目录，或者必须查找提供程序的跟踪消息的 [TMF 文件](trace-message-format-file.md) 。

TraceView 支持两种方法：

- 当您不确定要用于跟踪提供程序的 TMF 文件时，请使用 **SET TMF 搜索路径** 选项。 TraceView 搜索指定目录中的所有 TMF 文件，并将生成的消息的消息 GUID 与 TMF 文件的名称相匹配。 TMF 文件必须位于指定的目录中。 TraceView 不会以递归方式搜索。

- 当你知道要用于跟踪提供程序的 TMF 文件时，或者当你需要的 TMF 文件位于不同的目录时，请使用 " **选择 TMF 文件** " 选项。 如果 TMF 文件的名称不是 [消息 GUID](message-guid.md)，还必须使用此选项，因为 TraceView 在目录中找不到该文件。

如果指定的 TMF 文件或 TraceView 在指定目录中查找的文件与跟踪提供程序生成的跟踪消息不匹配，则 TraceView 无法对消息进行格式设置。 相反，它会显示跟踪消息 GUID 和以下错误消息：

```
No Format Information found.
```

若要从 PDB 符号文件创建 TMF 文件，请在命令提示符窗口中使用 [Tracepdb](tracepdb.md)。