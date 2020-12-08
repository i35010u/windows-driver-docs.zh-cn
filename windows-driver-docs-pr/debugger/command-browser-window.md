---
title: 在 WinDbg 中使用命令浏览器窗口
description: 在 WinDbg 中使用命令浏览器窗口
keywords:
- 调试信息窗口，命令浏览器窗口
- 命令浏览器窗口
- 调试器命令窗口，命令浏览器窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f7c1faad17192b86cec0149d2f2dfd477588a81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831985"
---
# <a name="using-the-command-browser-window-in-windbg"></a>在 WinDbg 中使用命令浏览器窗口


命令浏览器窗口显示并存储调试器命令的文本结果。 此窗口创建一个命令引用，使你能够在不重新输入命令的情况下查看特定命令的结果。 命令浏览器窗口还提供了通过存储的命令进行的导航，因此，与 [调试器命令窗口](debugger-command-window.md)相比，你可以更快地访问命令。

### <a name="span-idopening_the_command_browser_windowspanspan-idopening_the_command_browser_windowspanopening-the-command-browser-window"></a><span id="opening_the_command_browser_window"></span><span id="OPENING_THE_COMMAND_BROWSER_WINDOW"></span>打开 "命令浏览器" 窗口

你可以一次打开多个命令浏览器窗口。 若要打开命令浏览器窗口，请从 "**视图**" 菜单中选择 "**命令浏览器**"。  (还可以按 CTRL + N，或单击工具栏上 **的 "** ![ 命令浏览器") 按钮 (屏幕截图屏幕截图 ](images/window-command-browser-icon.png) 。 ALT + SHIFT + N 关闭命令浏览器窗口。 ) 

你还可以通过在 "浏览器" 中输入命令窗口 "浏览 [**(在浏览器中) 浏览显示命令**](-browse--display-command-in-browser-.md) 。

下面的屏幕截图显示了命令浏览器窗口的示例。

![命令浏览器窗口的屏幕截图](images/window-commandbrowser.png)

### <a name="span-idusing_the_command_browser_windowspanspan-idusing_the_command_browser_windowspanusing-the-command-browser-window"></a><span id="using_the_command_browser_window"></span><span id="USING_THE_COMMAND_BROWSER_WINDOW"></span>使用命令浏览器窗口

在命令浏览器窗口中，您可以执行以下操作：

-   若要输入命令，请在 " **命令** " 框中键入命令。

-   若要查看以前输入的命令的结果，请使用 " **开始**"、" **上** 一步" 和 " **下一步** " 按钮滚动浏览命令列表，或从 **命令** 菜单中选择前面的20个命令之一。 若要查找不是上述20个命令之一的命令，请使用 " **下一步** " 按钮。

命令浏览器窗口有一个快捷菜单，其中包含其他命令。 若要访问菜单，请右键单击标题栏或单击窗口右上角附近的图标 (![显示命令浏览器窗口工具栏快捷菜单的按钮屏幕截图](images/window-command-browser-icon.png)). 以下列表描述了一些菜单命令：

-   "**启动**"、"**上** 一步" 和 "**下一步**" 将光标移到命令历史记录的开头，或分别移动到上一个或下一个命令。

-   "**添加到最近的命令" 将** 当前命令放入 WinDbg 窗口中 "**查看**" 菜单的 "**最近使用的命令**" 菜单。 最近的命令保存在工作区中。

-   **工具栏** 打开和关闭工具栏。

-   **移动到新的停靠** 将关闭命令浏览器窗口，并在新的停靠中打开它。

-   **始终浮动** 会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   "**移动到帧**" 会导致在移动 WinDbg 帧时窗口移动，即使窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

在命令浏览器窗口中输入的命令由调试器引擎执行，而不是由 WinDbg 用户界面执行。 这意味着不能在命令浏览器窗口中输入用户界面命令，如 [**cls。**](-cls--clear-screen-.md) 如果用户界面是远程客户端，则服务器 (不是客户端) 执行命令。

在命令浏览器窗口中输入的命令将同步执行，因此直到完成后才会显示输出。

命令浏览器窗口保存在 WinDbg 工作区中，但不保存命令历史记录。 只有每个命令浏览器窗口的当前命令都保存在工作区中。

 

 





