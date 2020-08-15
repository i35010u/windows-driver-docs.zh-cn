---
title: 使用 WinDbg 打开转储文件
description: 可以通过多种方式来使用 WinDbg 打开转储文件。
ms.assetid: DE2EABE7-2B7A-4DF9-82FD-EF19D69E31A7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 655fa4a2f401fe09f6ae1e2db255f6a72d203240
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252837"
---
# <a name="opening-a-dump-file-using-windbg"></a>使用 WinDbg 打开转储文件


可以通过多种方式来使用 WinDbg 打开转储文件。

### <a name="span-idwindbg_menuspanspan-idwindbg_menuspanspan-idwindbg_menuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg 菜单

如果 WinDbg 已在运行并处于休眠模式，则可以通过从 "**文件**" 菜单中选择 "**打开故障转储**" 或按 CTRL + D 来打开转储。 出现 "打开故障转储" 对话框时，请在 **"文件名" 框中** 输入故障转储文件的完整路径和名称，或者使用 "" 对话框选择正确的路径和文件名。 选择了正确的文件后，选择 " **打开**"。

### <a name="span-idcommand_promptspanspan-idcommand_promptspanspan-idcommand_promptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符

在命令提示符窗口中，您可以在启动 WinDbg 时打开转储文件。 使用以下命令：

**windbg-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 (详细模式) 也很有用。 有关命令行语法的详细信息，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口

如果 WinDbg 已经在内核模式调试会话中，则可以使用 [**. opendump (打开转储文件) **](-opendump--open-dump-file-.md) 命令打开转储文件，后跟 [**g (") **](g--go-.md)"。

 

 





