---
title: 监视静默进程退出
description: 从 Windows 7 开始，您可以使用进程退出，无提示选项卡中 GFlags 输入想要监视无提示退出一个过程的名称。
ms.assetid: 116B2053-7F48-48B4-AEAC-333B7D9C38C7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51fdb8ff6afeb4350210b88450b1ce6ffbb5863d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353608"
---
# <a name="monitoring-silent-process-exit"></a>监视静默进程退出


从 Windows 7 开始，你可以使用**进程退出，无提示**GFlags 输入想要监视无提示退出一个过程的名称中的选项卡。

在此监视功能的上下文中，我们使用术语*无提示退出*表示受监视的进程中通过以下方式之一终止。

<span id="Self_termination"></span><span id="self_termination"></span><span id="SELF_TERMINATION"></span>自终止  
通过调用的受监控的进程终止自身**ExitProcess**。

<span id="Cross-process_termination"></span><span id="cross-process_termination"></span><span id="CROSS-PROCESS_TERMINATION"></span>跨进程终止  
第二个进程通过调用来终止受监视的进程**TerminateProcess**。

监视功能不会检测过程的最后一个线程退出时，会发生情况的普通进程终止。 监视功能不检测由内核模式代码启动的进程终止。

若要注册用于无提示退出监视进程，打开**进程退出，无提示**GFlags 中的选项卡。 输入进程名称作为**图像**然后按**选项卡**密钥。 检查**启用无提示进程退出监视**框中，然后单击**应用**。 这将设置 FLG\_监视器\_无提示\_进程\_退出标志在以下注册表项中的。

**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\图像 File Execution Options\\*ProcessName* \\GlobalFlag**

有关此标志的详细信息，请参阅[启用无提示的进程退出监视](enable-silent-process-exit-monitoring.md)。

有关使用详细信息**无提示的进程退出**GFlags 中选项卡上，请参阅[配置无提示进程退出监视](setting-and-clearing-flags-for-silent-process-exit.md)。

在中**无提示的进程退出**选项卡的 GFlags、 可以配置受监视的进程以无提示方式退出时将执行的操作。 你可以配置通知、 事件日志记录和创建转储文件。 你可以指定检测到无提示退出时，将启动一个进程，并可以指定的此监视器将忽略模块的列表。 在全局以及针对单个应用程序，这些设置的几个都可用。 全局设置适用于注册为无提示退出监视的所有进程。 应用程序设置应用于单个进程，并替代全局设置。

全局设置存储在以下项下的注册表。

**HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\SilentProcessExit**

应用程序设置存储在以下项下的注册表。

**HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\SilentProcessExit\\*ProcessName***

## <a name="span-idreportingmodespanspan-idreportingmodespanspan-idreportingmodespanreporting-mode"></a><span id="Reporting_Mode"></span><span id="reporting_mode"></span><span id="REPORTING_MODE"></span>报告模式


**报告模式**提供了设置为应用程序设置，但不能作为一种全局设置。 可以使用下面的复选框以设置报表模式。

**启动监视进程**
**启用转储收集**
**启用通知** **ReportingMode**注册表项是以下标志的按位 OR。

| Flag                   | 值 | 含义                                                                                                                                                                                            |
|------------------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 启动\_MONITORPROCESS | 0x1   | 检测到无提示退出时，监视进程 (在指定**监视器进程**框) 启动。                                                                                          |
| 本地\_转储            | 0x2   | 检测到无提示退出时，为受监视的进程创建转储文件。 在跨进程终止的情况下导致终止的进程还创建转储文件。 |
| 通知           | 0x4   | 检测到无提示退出时，会显示一个弹出通知。                                                                                                                                  |

 

## <a name="span-idignoreselfexitsspanspan-idignoreselfexitsspanspan-idignoreselfexitsspanignore-self-exits"></a><span id="Ignore_Self_Exits"></span><span id="ignore_self_exits"></span><span id="IGNORE_SELF_EXITS"></span>忽略自退出


**忽略自助退出**提供了设置为应用程序设置，但不能作为一种全局设置。 可以使用**忽略自退出**复选框以指定是否忽略自退出。

**IgnoreSelfExits**注册表项具有以下值之一。

| ReplTest1 | 含义                                                                    |
|-------|----------------------------------------------------------------------------|
| 0x0   | 检测和响应自终止和跨进程终止。 |
| 0x1   | 忽略自终止。 检测和响应跨进程终止。  |

 

## <a name="span-idmonitorprocessspanspan-idmonitorprocessspanspan-idmonitorprocessspanmonitor-process"></a><span id="Monitor_Process"></span><span id="monitor_process"></span><span id="MONITOR_PROCESS"></span>监视进程


可以通过输入进程名称，以及命令行参数中指定监视器进程**监视器进程**文本框。 在命令行中，可以使用以下变量。

| 变量 | 含义                                                                                                                                                                                                      |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| %e       | 正在退出的进程 ID。 这是以无提示方式退出受监视的进程。                                                                                                                               |
| %i       | 启动进程的 ID。 对于自身的终止时，这是与正在退出的过程相同。 对于跨进程终止时，这是进程的导致终止 ID。 |
| %t       | 启动线程的 ID。 这是导致终止的线程。                                                                                                                                  |
| %c       | 状态代码传递给**ExitThread**或**TerminateThread** 。                                                                                                                                            |

 

例如，以下值**监视器进程**指定无提示退出时，WinDbg 是启动和附加到正在退出的过程。

**windbg -p %e**

**监视器进程**命令行存储在**MonitorProcess**注册表项。

## <a name="span-iddumpfolderlocationspanspan-iddumpfolderlocationspanspan-iddumpfolderlocationspandump-folder-location"></a><span id="Dump_Folder_Location"></span><span id="dump_folder_location"></span><span id="DUMP_FOLDER_LOCATION"></span>转储的文件夹位置


可以使用**转储文件夹位置**文本框中，用于指定在检测到无提示退出时会写入临时文件的转储文件的位置。

您输入的字符串**转储文件夹位置**存储在**LocalDumpFolder**注册表项。

如果不指定转储文件夹位置，转储文件将写入默认位置，即 %TEMP%\\无提示的进程退出。

## <a name="span-iddumpfoldersizespanspan-iddumpfoldersizespanspan-iddumpfoldersizespandump-folder-size"></a><span id="Dump_Folder_Size"></span><span id="dump_folder_size"></span><span id="DUMP_FOLDER_SIZE"></span>转储文件夹的大小


可以使用**转储文件夹大小**文本框中指定的最大数的转储文件，可以写入转储文件夹。 输入此值为十进制整数。

您输入的值**转储文件夹的大小**存储在**MaximumNumberOfDumpFiles**注册表项。

默认情况下，可写入的转储文件数没有限制。

## <a name="span-iddumptypespanspan-iddumptypespanspan-iddumptypespandump-type"></a><span id="Dump_Type"></span><span id="dump_type"></span><span id="DUMP_TYPE"></span>转储类型


可以使用**转储类型**下拉列表来指定当检测到无提示退出时编写的转储文件 （Micro、 最小、 堆或自定义） 的类型。

转储类型存储在**DumpType**注册表项，这是按位或的成员**小型转储\_类型**枚举。 此枚举是在 dbghelp.h，包含有关 Windows 调试工具包中定义的。

例如，假设你选择了一种转储类型的**Micro**，并可以看到**DumpType**注册表项的值为 0x88。 0x88 的值是以下两个的按位 OR**小型转储\_类型**枚举值。

|                           |            |
|---------------------------|------------|
| MiniDumpFilterModulePaths | 0x00000080 |
| MiniDumpFilterMemory      | 0x00000008 |

 

如果您选择的转储类型**自定义**，输入你自己按位 OR**小型转储\_类型**中的枚举值**自定义转储类型**框。 输入此值为十进制整数。

## <a name="span-idmoduleignorelistspanspan-idmoduleignorelistspanspan-idmoduleignorelistspanmodule-ignore-list"></a><span id="Module_Ignore_List"></span><span id="module_ignore_list"></span><span id="MODULE_IGNORE_LIST"></span>模块忽略列表


可以使用**模块忽略列表**框以指定当检测到无提示退出时将忽略模块的列表。 如果在受监视的进程终止由某个模块在此列表中，将忽略无提示退出。

输入中的模块列表**模块忽略列表**框中将存储在**ModuleIgnoreList**注册表项。

## <a name="span-idreadingprocessexitreportsineventviewerspanspan-idreadingprocessexitreportsineventviewerspanspan-idreadingprocessexitreportsineventviewerspanreading-process-exit-reports-in-event-viewer"></a><span id="Reading_Process_Exit_Reports_in_Event_Viewer"></span><span id="reading_process_exit_reports_in_event_viewer"></span><span id="READING_PROCESS_EXIT_REPORTS_IN_EVENT_VIEWER"></span>在事件查看器中读取的进程退出报告


受监视的进程退出时以无提示方式，此监视器在事件查看器中创建的项。 若要打开事件查看器，请输入命令**eventvwr.msc**。 导航到**Windows 日志&gt;应用程序**。 查找具有的日志条目**源**的进程退出监视器。

![事件属性对话框显示常规选项卡显示源为进程退出监视器](images/gflagssilentprocessexit02.png)

 

 





