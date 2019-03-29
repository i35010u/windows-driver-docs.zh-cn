---
title: 使用 WinDbg 打开转储文件
description: 有几种方法可以使用 WinDbg 打开转储文件。
ms.assetid: DE2EABE7-2B7A-4DF9-82FD-EF19D69E31A7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45306cc5c78042d70bcf803ebe61abccdea0c8d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562082"
---
# <a name="opening-a-dump-file-using-windbg"></a>使用 WinDbg 打开转储文件


有几种方法可以使用 WinDbg 打开转储文件。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg Menu

如果 WinDbg 已在运行和处于休眠模式，则可以通过选择打开转储**打开崩溃转储**从**文件**菜单或通过按 CTRL + D。 打开故障转储对话框出现时，输入完整路径和崩溃转储文件中的名称**文件名**框中，或使用对话框中选择正确的路径和文件名称。 选择适当的文件后，单击**打开**。

### <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符

在命令提示符窗口中，可以打开转储文件，则在启动 WinDbg 时。 使用以下命令：

**windbg -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关命令行语法的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口

如果 WinDbg 已在内核模式调试会话中，您可以使用打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令后, 跟[ **g （转向）**](g--go-.md).

 

 





