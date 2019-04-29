---
title: 在 WinDbg 中设置断点
description: 有几种方法可以设置、 查看和操作使用 WinDbg 的断点。
ms.assetid: 4A7BE6D2-05AF-4EFB-8F24-C19B1A98217C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cfdeb439a342d0dc328842621dc34f89cd567da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381959"
---
# <a name="setting-breakpoints-in-windbg"></a>在 WinDbg 中设置断点


有几种方法可以设置、 查看和操作使用 WinDbg 的断点。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以设置、 查看和操作调试器命令窗口中输入命令断点。 有关命令的列表，请参阅[控制断点方法](methods-of-controlling-breakpoints.md)。

## <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg Menu


您可以打开**断点**对话框中，通过选择**断点**从**编辑**菜单或通过按 ALT + F9。 此对话框列出了所有断点，并禁用、 启用或清除现有断点或设置新断点，可以使用它。

## <a name="span-idcodewindowsspanspan-idcodewindowsspanspan-idcodewindowsspancode-windows"></a><span id="Code_Windows"></span><span id="code_windows"></span><span id="CODE_WINDOWS"></span>代码 Windows


反汇编窗口和源窗口突出显示设置了断点的行。 已启用的断点为红色，并已禁用的断点处于黄色。

如果将光标设置在反汇编窗口中或在源窗口中的特定行上，可以按 F9 在该行上设置断点。

 

 





