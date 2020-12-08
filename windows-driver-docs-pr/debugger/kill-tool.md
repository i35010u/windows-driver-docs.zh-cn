---
title: 终止工具
description: Kill 工具 kill.exe 终止一个或多个进程及其所有线程。 此工具仅适用于在本地计算机上运行的进程。
keywords: kill 工具、Kill.exe、kill.exe
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9b00ec69e8c311c99a4c1da96d3f7860a9b5d41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806543"
---
# <a name="kill-tool"></a>终止工具

Kill 工具 kill.exe 终止一个或多个进程及其所有线程。 此工具仅适用于在本地计算机上运行的进程。

## <a name="span-idwhere_to_get_kill_toolspanspan-idwhere_to_get_kill_toolspanspan-idwhere_to_get_kill_toolspanwhere-to-get-kill-tool"></a><span id="Where_to_get_Kill_Tool"></span><span id="where_to_get_kill_tool"></span><span id="WHERE_TO_GET_KILL_TOOL"></span>获取终止工具的位置

Kill.exe 包含在 [Windows 调试工具](index.md)中。

## <a name="span-idkill_tool_command-line_optionsspanspan-idkill_tool_command-line_optionsspanspan-idkill_tool_command-line_optionsspankill-tool-command-line-options"></a><span id="Kill_Tool_command-line_options"></span><span id="kill_tool_command-line_options"></span><span id="KILL_TOOL_COMMAND-LINE_OPTIONS"></span>Kill 工具命令行选项

```console
kill [/f] { PID | Pattern* }
```

### <a name="span-idddk_kill_tool_commands_dtoolsspanspan-idddk_kill_tool_commands_dtoolsspanparameters"></a><span id="ddk_kill_tool_commands_dtools"></span><span id="DDK_KILL_TOOL_COMMANDS_DTOOLS"></span>参数

<span id="________f______"></span><span id="________F______"></span>**/f** 强制终止进程，而不提示用户进行确认。 需要使用此选项来终止受保护的进程，例如系统服务。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID* 指定要终止的任务 (PID) 的进程标识符。

若要查找任务的 PID，请在 Microsoft Windows XP 和更高版本或 Windows 2000 的 [tlist.exe](tlist.md) 中使用 TaskList。

<span id="_______Pattern_"></span><span id="_______pattern_"></span><span id="_______PATTERN_"></span><em>Pattern</em> * 模式 *\** _  
指定任务或窗口的全部或部分名称。 Kill 工具终止进程名称或窗口名称与模式匹配的所有进程。 星号是必需的。

在使用可能会无意中匹配多个进程或窗口名称的模式之前，请使用 _ *tlist.exe* *  *模式* 命令测试模式。 有关详细信息，请参阅 [tlist.exe](tlist.md) 。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例

以下命令终止名称以 "myapp" 开头的进程。

```console
kill myapp*
```

以下命令终止进程 ID (PID) 为2520的进程：

```console
kill 2520
```

以下命令终止名称以 "my" 开头的进程 \* 。 它不提示确认。 即使此进程是系统服务，此命令也会成功：

```console
kill /f my*
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[Windows 调试工具中包含的工具](extra-tools.md)
