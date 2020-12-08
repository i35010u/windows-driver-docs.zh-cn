---
title: 在 WinDbg 中设置断点
description: 可以通过多种方式使用 WinDbg 设置、查看和处理断点。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46a32921cb632d2970fbe6f82fdea3a8168df144
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828835"
---
# <a name="setting-breakpoints-in-windbg"></a>在 WinDbg 中设置断点


可以通过多种方式使用 WinDbg 设置、查看和处理断点。

## <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


您可以通过在调试器命令窗口中输入命令来设置、查看和操作断点。 有关命令的列表，请参阅 [控制断点的方法](methods-of-controlling-breakpoints.md)。

## <a name="span-idwindbg_menuspanspan-idwindbg_menuspanspan-idwindbg_menuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg 菜单


通过选择 "**编辑**" 菜单中的 "**断点**" 或按 ALT + F9，可以打开 "**断点**" 对话框。 此对话框列出了所有断点，您可以使用它来禁用、启用或清除现有断点，或设置新断点。

## <a name="span-idcode_windowsspanspan-idcode_windowsspanspan-idcode_windowsspancode-windows"></a><span id="Code_Windows"></span><span id="code_windows"></span><span id="CODE_WINDOWS"></span>代码窗口


"反汇编" 窗口和 "源窗口" 突出显示已设置断点的行。 启用的断点为红色，禁用的断点为黄色。

如果在 "反汇编" 窗口或源窗口中的特定行上设置光标，则可以按 F9 在该行设置断点。

 

 





