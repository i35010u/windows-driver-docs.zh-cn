---
title: 监视静默进程退出
description: 从 Windows 7 开始，你可以使用 GFlags 中的 "无提示处理退出" 选项卡，输入要监视以进行无提示退出的进程的名称。
ms.assetid: 116B2053-7F48-48B4-AEAC-333B7D9C38C7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a484cc76779b438b609778d39f12548d0aa4697d
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253095"
---
# <a name="monitoring-silent-process-exit"></a>监视静默进程退出


从 Windows 7 开始，你可以使用 GFlags 中的 " **无提示处理退出** " 选项卡，输入要监视以进行无提示退出的进程的名称。

在此监视功能的上下文中，我们使用术语 " *无提示退出* " 表示受监视的进程通过以下方式之一终止。

<span id="Self_termination"></span><span id="self_termination"></span><span id="SELF_TERMINATION"></span>自行终止  
受监视的进程通过调用 **ExitProcess**自行终止。

<span id="Cross-process_termination"></span><span id="cross-process_termination"></span><span id="CROSS-PROCESS_TERMINATION"></span>跨进程终止  
第二个进程通过调用 **TerminateProcess**终止监视的进程。

监视功能不检测在进程的最后一个线程退出时发生的正常进程终止。 监视功能不检测由内核模式代码启动的进程终止。

若要注册用于无提示退出监视的进程，请打开 GFlags 中的 " **无提示处理退出** " 选项卡。 输入进程名称作为 **图像** ，然后按 **tab** 键。 选中 " **启用无提示进程退出监视** " 框，然后选择 " **应用**"。 这会 \_ \_ \_ 在以下注册表项中设置 FLG 监视器无提示处理 \_ 退出标志。

**HKLM \\ SOFTWARE \\ MICROSOFT \\ Windows NT \\ CurrentVersion \\ Image File 执行选项 \\ *ProcessName* \\ GlobalFlag**

有关此标志的详细信息，请参阅 [启用无提示进程退出监视](enable-silent-process-exit-monitoring.md)。

有关使用 GFlags 中的 " **无提示处理退出** " 选项卡的详细信息，请参阅 [配置无提示进程退出监视](setting-and-clearing-flags-for-silent-process-exit.md)。

在 GFlags 的 " **无提示处理退出** " 选项卡中，你可以配置当监视的进程无提示退出时将发生的操作。 你可以配置通知、事件日志记录和转储文件的创建。 可以指定在检测到无提示退出时启动的进程，还可以指定监视器将忽略的模块的列表。 其中的多个设置在全局和单个应用程序中均可用。 全局设置适用于为无提示退出监视注册的所有进程。 应用程序设置适用于单个进程并重写全局设置。

全局设置存储在注册表中的以下项下。

**HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ SilentProcessExit**

应用程序设置存储在注册表中的以下项下。

**HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ SilentProcessExit \\ * ProcessName***

## <a name="span-idreporting_modespanspan-idreporting_modespanspan-idreporting_modespanreporting-mode"></a><span id="Reporting_Mode"></span><span id="reporting_mode"></span><span id="REPORTING_MODE"></span>报告模式


**报表模式**设置可用作应用程序设置，但不能作为全局设置。 您可以使用以下复选框来设置报告模式。

**启动监视器进程** 
**启用转储收集** 
**启用通知****ReportingMode**注册表项是以下标志的按位 "或"。

| 标志                   | 值 | 含义                                                                                                                                                                                            |
|------------------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 启动 \_ MONITORPROCESS | 0x1   | 检测到缄默 exit 时，会启动 " **监视进程** " 框中 (指定的监视器进程) 。                                                                                          |
| 本地 \_ 转储            | 0x2   | 检测到缄默 exit 时，将为监视的进程创建转储文件。 对于跨进程终止，还会为导致终止的进程创建转储文件。 |
| 通知           | 0x4   | 当检测到缄默 exit 时，将显示一个弹出通知。                                                                                                                                  |

 

## <a name="span-idignore_self_exitsspanspan-idignore_self_exitsspanspan-idignore_self_exitsspanignore-self-exits"></a><span id="Ignore_Self_Exits"></span><span id="ignore_self_exits"></span><span id="IGNORE_SELF_EXITS"></span>忽略自退出


" **忽略自退出** " 设置可用作应用程序设置，但不能作为全局设置。 您可以使用 " **忽略自退出** " 复选框来指定是否忽略己方退出。

**IgnoreSelfExits**注册表项具有以下值之一。

| 值 | 含义                                                                    |
|-------|----------------------------------------------------------------------------|
| 0x0   | 检测并响应自我终止和跨进程终止。 |
| 0x1   | 忽略自终止。 检测并响应跨进程终止。  |

 

## <a name="span-idmonitor_processspanspan-idmonitor_processspanspan-idmonitor_processspanmonitor-process"></a><span id="Monitor_Process"></span><span id="monitor_process"></span><span id="MONITOR_PROCESS"></span>监视进程


您可以通过在 " **监视进程** " 文本框中输入进程名称和命令行参数来指定监视进程。 您可以在命令行中使用以下变量。

| 变量 | 含义                                                                                                                                                                                                      |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| % e       | 正在退出的进程的 ID。 这是在无提示的情况下被监视的进程。                                                                                                                               |
| % i       | 启动进程的 ID。 对于自行终止，这与退出过程相同。 对于跨进程终止，这是导致终止的进程的 ID。 |
| % t       | 启动线程的 ID。 这是导致终止的线程。                                                                                                                                  |
| % c       | 传递给 **ExitThread** 或 **TerminateThread** 的状态代码。                                                                                                                                            |

 

例如，以下 **监视进程** 值指定在无提示退出时，WinDbg 将启动并附加到现有进程。

**windbg-p% e**

" **监视进程** " 命令行存储在 **MonitorProcess** 注册表项中。

## <a name="span-iddump_folder_locationspanspan-iddump_folder_locationspanspan-iddump_folder_locationspandump-folder-location"></a><span id="Dump_Folder_Location"></span><span id="dump_folder_location"></span><span id="DUMP_FOLDER_LOCATION"></span>转储文件夹位置


可以使用 " **转储文件夹位置** " 文本框指定在检测到无提示退出时写入的转储文件的位置。

你为 **转储文件夹位置** 输入的字符串存储在 **LocalDumpFolder** 注册表项中。

如果未指定转储文件夹位置，则转储文件将写入到默认位置，即% TEMP% \\ 缄默进程退出。

## <a name="span-iddump_folder_sizespanspan-iddump_folder_sizespanspan-iddump_folder_sizespandump-folder-size"></a><span id="Dump_Folder_Size"></span><span id="dump_folder_size"></span><span id="DUMP_FOLDER_SIZE"></span>转储文件夹大小


您可以使用 " **转储文件夹大小** " 文本框指定可以写入转储文件夹的转储文件的最大数目。 将此值输入为十进制整数。

你为 **转储文件夹大小** 输入的值存储在 **MaximumNumberOfDumpFiles** 注册表项中。

默认情况下，可写入的转储文件数没有限制。

## <a name="span-iddump_typespanspan-iddump_typespanspan-iddump_typespandump-type"></a><span id="Dump_Type"></span><span id="dump_type"></span><span id="DUMP_TYPE"></span>转储类型


可以使用 " **转储类型** " 下拉列表来指定在检测到无提示退出时写入 (微、微型、堆或自定义) 的转储文件的类型。

转储类型存储在 **DumpType** 注册表项中，后者是 **小型转储 \_ 类型** 枚举成员的按位 "或"。 此枚举是在 dbghelp.dll 中定义的，它包含在 Windows 包的调试工具中。

例如，假设你选择了 " **微**转储类型"，你会看到 " **DumpType** " 注册表项的值为 "0x88"。 值0x88 是以下两个 **小型转储 \_ 类型** 枚举值的按位 "或"。

**MiniDumpFilterModulePaths**：0x00000080

**MiniDumpFilterMemory**：0x00000008


 

如果选择 "**自定义**" 转储类型，请在 "**自定义转储类型**" 框中输入你自己的**小型转储 \_ 类型**枚举值的按位或。 将此值输入为十进制整数。

## <a name="span-idmodule_ignore_listspanspan-idmodule_ignore_listspanspan-idmodule_ignore_listspanmodule-ignore-list"></a><span id="Module_Ignore_List"></span><span id="module_ignore_list"></span><span id="MODULE_IGNORE_LIST"></span>模块忽略列表


您可以使用 " **模块忽略" 列表** 框来指定在检测到缄默退出时将被忽略的模块的列表。 如果此列表中的某个模块终止了监视的进程，则会忽略缄默退出。

在 " **模块忽略" 列表** 框中输入的模块列表存储在 **ModuleIgnoreList** 注册表项中。

## <a name="span-idreading_process_exit_reports_in_event_viewerspanspan-idreading_process_exit_reports_in_event_viewerspanspan-idreading_process_exit_reports_in_event_viewerspanreading-process-exit-reports-in-event-viewer"></a><span id="Reading_Process_Exit_Reports_in_Event_Viewer"></span><span id="reading_process_exit_reports_in_event_viewer"></span><span id="READING_PROCESS_EXIT_REPORTS_IN_EVENT_VIEWER"></span>读取事件查看器中的进程退出报表


当监视的进程无提示退出时，监视器将在事件查看器中创建一个条目。 若要打开事件查看器，请输入 **eventvwr.msc**命令。 导航到 " **Windows 日志" &gt; 应用程序**。 查找具有进程退出监视器的 **源** 的日志条目。

![显示 "常规" 选项卡的 "事件属性" 对话框将源显示为进程退出监视器](images/gflagssilentprocessexit02.png)

 

 





