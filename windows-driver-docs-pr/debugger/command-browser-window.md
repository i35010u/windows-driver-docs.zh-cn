---
title: 使用命令浏览器窗口在 WinDbg 中
description: 使用命令浏览器窗口在 WinDbg 中
ms.assetid: b895f463-38ec-451a-8c0a-0deb8650a904
keywords:
- 调试信息窗口中，命令浏览器窗口
- 命令浏览器窗口
- 调试器命令窗口中，命令浏览器窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fd0e489b10125f6ef2174aa80c65a8a7a1a8bca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523392"
---
# <a name="using-the-command-browser-window-in-windbg"></a>使用命令浏览器窗口在 WinDbg 中


命令浏览器窗口中显示，并将存储的调试器命令文本结果。 此窗口创建可用于查看特定命令的结果，而无需重新输入该命令的命令参考。 命令浏览器窗口中还提供了通过存储命令导航、 详细信息以便您可以快速访问具有比命令[调试器命令窗口](debugger-command-window.md)。

### <a name="span-idopeningthecommandbrowserwindowspanspan-idopeningthecommandbrowserwindowspanopening-the-command-browser-window"></a><span id="opening_the_command_browser_window"></span><span id="OPENING_THE_COMMAND_BROWSER_WINDOW"></span>打开命令浏览器窗口

可以一次打开多个命令浏览器窗口。 若要打开命令浏览器窗口，请选择**命令浏览器**从**视图**菜单。 (还可以按 CTRL + N，或单击**命令浏览器**按钮 (![命令浏览器按钮的屏幕截图](images/window-command-browser-icon.png)) 工具栏上。 ALT + SHIFT + N 关闭命令浏览器窗口）。

此外可以打开一个命令浏览器窗口，通过输入[ **.browse （在浏览器中显示命令）** ](-browse--display-command-in-browser-.md)常规调试器命令窗口中。

以下屏幕截图显示命令浏览器窗口的一个示例。

![命令浏览器窗口的屏幕截图](images/window-commandbrowser.png)

### <a name="span-idusingthecommandbrowserwindowspanspan-idusingthecommandbrowserwindowspanusing-the-command-browser-window"></a><span id="using_the_command_browser_window"></span><span id="USING_THE_COMMAND_BROWSER_WINDOW"></span>使用命令浏览器窗口

在命令浏览器窗口中，可以执行以下操作：

-   若要输入命令时，其在键入**命令**框。

-   若要查看以前输入的命令的结果，请使用**启动**， **Prev**，并**下一步**按钮来滚动查看命令列表，或选择其中一个的前 20 个从命令**命令**菜单。 若要查找不是一个前面的 20 个命令的命令，使用**下一步**按钮。

命令浏览器窗口具有带其他命令的快捷菜单。 若要访问菜单，请右键单击标题栏或单击窗口 （在右上角附近的图标![该按钮将显示命令浏览器窗口中工具栏快捷方式菜单的屏幕截图](images/window-command-browser-icon.png))。 以下列表介绍了一些菜单命令：

-   **启动**， **Prev**，和**下一步**将光标移动到起始位置的命令历史记录或添加到上一个或下一个命令，分别。

-   **将添加到新的命令**放入到当前命令**新的命令**菜单**视图**WinDbg 窗口中的菜单。 新的命令保存在工作区中。

-   **工具栏**工具栏，开启和关闭。

-   **移到新停靠**关闭命令浏览器窗口并将其打开新的平台中。

-   **始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   **移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

由调试器引擎，不是由 WinDbg 用户界面执行的命令浏览器窗口中输入的命令。 这意味着不能输入用户界面命令，例如[ **.cls** ](-cls--clear-screen-.md)命令浏览器窗口中。 如果用户界面，远程客户端服务器 （而不是客户端） 执行的命令。

命令浏览器窗口中输入的命令执行同步，因此它不会显示输出，直到它完成。

命令的浏览器窗口都保存在 WinDbg 工作区中，但不是会保存命令历史记录。 仅适用于每个命令浏览器窗口的当前命令保存在工作区。

 

 





