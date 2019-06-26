---
title: TraceView 的概念
description: TraceView 的概念
ms.assetid: 4fab2b23-8f7b-407b-b944-41ac8caf1a75
keywords:
- TraceView WDK 术语
- 跟踪会话 WDK，组
- 分组跟踪会话
- 有关工作区的工作区 WDK TraceView，
- 跟踪会话 WDK，工作区
- 跟踪提供程序 WDK
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
- TMF 文件 WDK，搜索路径
- 搜索路径 WDK 软件跟踪
- TMF 文件 WDK，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 224175f90d526d5d54d7632334809f0c3b80f4d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363814"
---
# <a name="traceview-concepts"></a>TraceView 的概念

## <span id="ddk_traceview_concepts_tools"></span><span id="DDK_TRACEVIEW_CONCEPTS_TOOLS"></span>

本主题介绍在 TraceView 中使用的概念。

有关通用的 WDK 中的跟踪工具的概念信息，请参阅[跟踪工具概念](tracing-tool-concepts.md)。

### <a name="span-idtracesessiongroupspanspan-idtracesessiongroupspanspan-idtracesessiongroupspantrace-session-group"></a><span id="Trace_Session_Group"></span><span id="trace_session_group"></span><span id="TRACE_SESSION_GROUP"></span>跟踪会话组

TraceView 可让你组合[跟踪日志](trace-log.md)显示或到实时跟踪会话*跟踪会话组*并管理它们，就好像它们是单个会话。 当跟踪日志或会话位于同一个跟踪会话组，其消息组合在一个[跟踪消息列表](trace-message-lists.md)。

默认情况下，每个跟踪会话是包含仅该跟踪会话的跟踪会话组的成员。

有关创建跟踪会话组的信息，请参阅[分组跟踪会话](grouping-trace-sessions.md)。

### <a name="span-idworkspacespanspan-idworkspacespanspan-idworkspacespanworkspace"></a><span id="Workspace"></span><span id="workspace"></span><span id="WORKSPACE"></span>工作区

在 TraceView，*工作区*是一组跟踪会话属性和跟踪日志可以保存并重复使用的显示属性。 对于工作区，可以显示常用的日志或在一个快速的步骤中启动仔细配置的跟踪会话。

工作区包括：

- 跟踪会话，包括缓冲区、 标志和级别，以及跟踪日志的位置的所有属性

- 位置[程序数据库 (PDB) 符号文件](pdb-symbol-files.md)，[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)，或 TMF 搜索路径

- 列出文件和摘要文件 TraceView 的路径和文件名称

- [筛选器](filtering-trace-messages.md)

实时跟踪会话中打开工作区时，TraceView 启动新的跟踪会话使用已保存的属性和配置设置。 当您打开的工作区的显示跟踪日志时，必须将其配置的样子，此时将显示日志。

有关详细信息，请参阅[使用 TraceView 工作区](using-traceview-workspaces.md)。

### <a name="span-idspecifyingtraceprovidersspanspan-idspecifyingtraceprovidersspanspan-idspecifyingtraceprovidersspanspecifying-trace-providers"></a><span id="Specifying_Trace_Providers"></span><span id="specifying_trace_providers"></span><span id="SPECIFYING_TRACE_PROVIDERS"></span>指定跟踪提供程序

若要创建一个跟踪会话，必须确定跟踪提供程序，并找到提供程序生成的二进制跟踪消息的格式设置说明。 您可以执行此任一通过以下方式操作：

- 找到行提供程序的源代码可执行文件的二进制文件。 TraceView 可以提取所有启用和设置的格式所需的信息[TraceLogging](https://docs.microsoft.com/windows/desktop/tracelogging/trace-logging-portal)和列入清单的 ETW 事件。 它也会尝试查找[PDB 符号文件](pdb-symbol-files.md)要启用任意[WPP 软件跟踪](wpp-software-tracing.md)提供程序。

- 找到[PDB 符号文件](pdb-symbol-files.md)包含的源代码[WPP 软件跟踪](wpp-software-tracing.md)提供程序。 TraceView 可以从在 PDB 中提取文件的所有信息，需要标识提供者并设置其跟踪消息的格式。

- 找到[控制 GUID (.ctl) 文件](control-guid-file.md)提供程序，并指定[TMF 文件](trace-message-format-file.md)或存储 TMF 文件的目录的路径。

- 输入[控制 GUID](control-guid.md)的提供程序，并指定 TMF 文件或存储 TMF 文件的目录的路径。

    如果你输入前面标有星号的提供程序名称 (例如```*SampleProvider```)，TraceView 自动将名称转换使用某种标准算法的 GUID。 并非所有提供程序遵循这个标准，但很多，例如提供程序使用编写[。NET 的 EventSource](https://docs.microsoft.com/dotnet/api/system.diagnostics.tracing.eventsource?view=netframework-4.8)，执行操作。

- 选择[注册的提供程序](registered-provider.md)从列表中该 TraceView 组装并指定 TMF 文件或存储 TMF 文件的目录的路径。

- 选择[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，然后选择一个或多个操作系统事件跟踪。

### <a name="span-idsettmfsearchpathandselecttmffilesoptionsspanspan-idsettmfsearchpathandselecttmffilesoptionsspanspan-idsettmfsearchpathandselecttmffilesoptionsspanset-tmf-search-path-and-select-tmf-files-options"></a><span id="Set_TMF_Search_Path_and_Select_TMF_Files_Options"></span><span id="set_tmf_search_path_and_select_tmf_files_options"></span><span id="SET_TMF_SEARCH_PATH_AND_SELECT_TMF_FILES_OPTIONS"></span>设置 TMF 搜索路径和选择 TMF 文件选项

在启用 WPP 提供程序，除非你有[PDB 符号文件](pdb-symbol-files.md)提供程序，必须指定在其中 TraceView 可以找到 TMF 文件，或必须找到一个目录[TMF 文件](trace-message-format-file.md)的提供程序的跟踪消息。

TraceView 支持两种方法：

- 使用**设置 TMF 搜索路径**选项时不能确定哪些 TMF 文件用于跟踪提供程序。 TraceView 搜索所有 TMF 文件中指定的目录和消息到 TMF 文件的名称生成消息的 GUID 匹配。 TMF 文件必须位于指定目录中。 TraceView 不会搜索以递归方式。

- 使用**选择 TMF 文件**选项时知道 TMF 文件用于跟踪提供程序，或当所需的 TMF 文件位于不同的目录中。 您还必须使用此选项，如果 TMF 文件的名称不是[消息 GUID](message-guid.md)，这是因为 TraceView 找不到它的目录中。

如果指定 TMF 文件或在指定的目录中查找 TraceView 与生成的跟踪提供程序的跟踪消息不匹配，TraceView 无法格式化消息。 相反，它会显示跟踪消息的 GUID 并显示以下错误消息：

```
No Format Information found.
```

若要从 PDB 符号文件，在命令提示符窗口中，创建 TMF 文件使用[Tracepdb](tracepdb.md)。
