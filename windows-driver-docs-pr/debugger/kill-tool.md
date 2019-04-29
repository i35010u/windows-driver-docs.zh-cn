---
title: 终止工具
description: Kill 工具、 kill.exe，终止一个或多个进程和所有其线程。 此工具仅适用于在本地计算机上运行的进程。
ms.assetid: e1733a74-2a31-436f-87b8-e704b27b6f04
keywords: 终止工具、 Kill.exe、 kill.exe
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c7683249757252908f23d8e58b5ca7cafad884
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376784"
---
# <a name="kill-tool"></a>终止工具


Kill 工具、 kill.exe，终止一个或多个进程和所有其线程。 此工具仅适用于在本地计算机上运行的进程。

## <a name="span-idwheretogetkilltoolspanspan-idwheretogetkilltoolspanspan-idwheretogetkilltoolspanwhere-to-get-kill-tool"></a><span id="Where_to_get_Kill_Tool"></span><span id="where_to_get_kill_tool"></span><span id="WHERE_TO_GET_KILL_TOOL"></span>获取终止工具的位置


中包含 Kill.exe[有关 Windows 调试工具](index.md)。

## <a name="span-idkilltoolcommand-lineoptionsspanspan-idkilltoolcommand-lineoptionsspanspan-idkilltoolcommand-lineoptionsspankill-tool-command-line-options"></a><span id="Kill_Tool_command-line_options"></span><span id="kill_tool_command-line_options"></span><span id="KILL_TOOL_COMMAND-LINE_OPTIONS"></span>终止工具命令行选项


```console
kill [/f] { PID | Pattern* }
```

### <a name="span-idddkkilltoolcommandsdtoolsspanspan-idddkkilltoolcommandsdtoolsspanparameters"></a><span id="ddk_kill_tool_commands_dtools"></span><span id="DDK_KILL_TOOL_COMMANDS_DTOOLS"></span>参数

<span id="________f______"></span><span id="________F______"></span> **/f**   
强制终止进程，而不提示用户进行确认。 此选项需要终止受保护的进程，如系统服务。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
指定任务要终止的进程标识符 (PID)。

若要查找任务的 PID，请使用 TaskList 中 Microsoft Windows XP 及更高版本或[TList](tlist.md) Windows 2000 中。

<span id="_______Pattern_"></span><span id="_______pattern_"></span><span id="_______PATTERN_"></span> <em>Pattern</em>**\\***  
指定所有或部分任务或窗口的名称。 Kill 工具终止所有进程的进程名称或窗口名称与模式匹配。 星号是必需的。

在使用之前可能会无意中匹配多个进程或窗口名称的模式，使用**tlist** *模式*命令测试模式。 请参阅[TList](tlist.md)有关详细信息。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


以下命令终止的进程的名称开头"myapp"。

```console
kill myapp*
```

以下命令会终止的进程的进程 ID (PID) 是 2520年:

```console
kill 2520
```

以下命令终止的进程的名称开头"我\*。" 它不会提示进行确认。 此命令成功，即使此过程是一种系统服务：

```console
kill /f my*
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 






