---
title: 使用 WinDbg 预览版进行调试
description: 本部分介绍如何执行基本使用 WinDbg 预览调试程序的调试任务。
ms.date: 10/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 103c62d0e878c7d8d46a174ec07374192e1cec84
ms.sourcegitcommit: c340d6058fa3ea6407d0041de80482b88f623a90
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59534155"
---
![Windbg preview 上的小徽标](images/windbgx-preview-logo.png) 

# <a name="debugging-using-windbg-preview"></a>使用 WinDbg 预览版进行调试 

WinDbg 预览版是与更现代的视觉对象、 更快的 windows、 功能齐全的脚本编写体验，使用可扩展的调试程序数据模型前面和中心构建的全新版本的 WinDbg。 WinDbg 预览使用同一个基础引擎作为 WinDbg 今天，因此所有命令、 扩展和您所习惯的工作流将仍可以正常都运行与以前一样。

有关最新新闻、 提示和从调试器开发团队的技巧，请参阅调试器工具团队博客。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)


## <a name="major-features-of-windbg-preview"></a>WinDbg Preview 的主要功能

下面是一些已更改或新增的最值得注意的事情。

![在调试器中的主屏幕](images/windbgx-main-menu.png)


### <a name="general-features"></a>常规功能

- **更轻松的连接设置和召回率**-WinDbg 预览版包括重新调用以前的会话配置信息的功能。

![在调试器中的主屏幕的屏幕截图](images/windbgx-start-debugging-menu.png)

- **轻松反馈通道**-你的反馈将指导今后在开发工作。 有关详细信息，请参阅[提供反馈](#providing-feedback)

- **转储文件处理器检测**-自动的检测到处理器体系结构，更轻松地托管调试。

- **性能改进**Windows 现在以异步方式加载，并可以取消-在运行另一个命令，WinDbg 预览时将停止在局部变量、 监视或其他窗口的加载。

### <a name="windowing-improvements"></a>窗口化改进

- **反汇编窗口改进**-还改进了反汇编窗口，突出显示的当前指令保持其所在滚动时。 

    ![在调试器中的反汇编窗口](images/windbgx-disassembly.png)


- **内存窗口改进**-内存窗口已突出显示和改进的滚动。

- **局部变量和监视数据模型可视化**-局部变量和监视窗口基于从 dx 命令使用的数据模型。 这意味着局部变量和监视窗口将受益于任何 NatVis 或 JavaScript 扩展已加载，并可以甚至支持完整 LINQ 查询，就像 dx 命令一样。 

- **日志**-这是在 WinDbg 预览内部机制的后台日志。 进行故障排除或长时间运行的进程监视器可以查看该规范。 

有关详细信息，请参阅[WinDbg 预览的视图菜单](windbg-view-preview.md)。

- **命令窗口**-使用命令窗口可轻松访问切换 DML 和清除与调试器命令窗口。 所有当前的调试器命令与兼容，并继续在 WinDbg 预览版中工作。


### <a name="dark-theme"></a>深色主题 

使用**文件** > **设置**若要启用深色主题。

![屏幕截图显示深色主题](images/windbgx-dark-theme.png)


### <a name="ribbon-quick-access"></a>功能区快速访问

只需将固定最常用的按钮和可折叠功能区保存的屏幕空间。 
 
![显示固定的项与 ribon 的屏幕截图](images/windbgx-quick-access.png)



### <a name="source-window"></a>源窗口

已更新源窗口为更加符合现代编辑器。 

![在调试器中的脚本编写菜单的屏幕截图](images/windbgx-source-window.png)


### <a name="highlighting"></a>突出显示

在命令窗口具有两个新的突出显示功能。 选择任何文本将授予细微突出显示该文本的任何其他实例。 然后可以按"突出显示突出显示/取消"或 Ctrl + Alt + H 继续将突出显示。 

![显示列以黄色突出显示的屏幕截图](images/windbgx-highlighting.gif)


### <a name="better-keyboard-navigation"></a>更好的键盘导航

只需按 Ctrl + Tab 和可以只是键盘与 windows 之间轻松导航。 

![屏幕截图显示 ctrl 选项卡菜单](images/windbgx-ctrl-tab.gif)


### <a name="integrated-time-travel-debugging-ttd"></a>集成的时间顺序查看调试 (TTD)

如果您需要 TTD 跟踪的应用程序，只需选中"并进行时间旅行调试记录过程"框时启动或附加。 WinDbgNext 将设置它，以便 TTD 并完成后打开的跟踪记录。

![屏幕截图显示 ctrl 选项卡菜单](images/windbgx-ttd.png)

有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


### <a name="debugging-app-packages"></a>调试应用包

调试你的通用应用程序或后台任务现在是一次单击。

![启动应用程序打包应用程序选项卡显示在搜索框中列出的三个应用 cal](images/windbgx-launch-app-package.png)

有关详细信息，请参阅[启动应用包](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)。


### <a name="attach-to-a-process"></a>附加到进程

附加对话框速度更快，更详细，并易于使用。

![将附加到进程对话框](images/windbgx-attach-to-a-process-zoomed.png)


### <a name="enhanced-breakpoint-tracking"></a>跟踪的增强的断点  

- **启用/禁用断点**-断点窗口显示您当前的所有断点，并可轻松访问到启用和禁用它们。 
- **命中计数**-断点窗口一直保持运行的总的每次命中断点。

有关详细信息，请参阅[断点](windbg-breakpoints-preview.md)。


### <a name="enhanced-data-model-support"></a>增强的数据模型支持

- **内置数据模型支持**-WinDbg 预览版编写使用内置的数据模型支持，数据模型可通过 out 调试器。
- **模型窗口**-模型窗口提供 dx 的可展开和可浏览版本和 dx-g，让你创建功能强大表之上的 NatVis、 JavaScript 和 LINQ 查询。 

有关详细信息，请参阅[WinDbg 预览版-数据模型](windbg-data-model-preview.md)。

![在调试器中的数据模型菜单的屏幕截图](images/windbgx-data-model-menu.png)


### <a name="new-scripting-development-ui"></a>新的脚本开发用户界面 

- **脚本开发用户界面**-没有专门构建的脚本窗口，来简化开发的 JavaScript 和 NatVis 脚本，与错误突出显示和 IntelliSense。

![在调试器中的脚本编写菜单的屏幕截图](images/windbgx-scripting-intellisense.png)

有关详细信息，请参阅[WinDbg 预览版-脚本](windbg-scripting-preview.md)。

### <a name="backwards-compatibility"></a>向后兼容性 

基础调试程序引擎是相同的因为所有以前的调试器命令和调试器扩展继续工作。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>提供反馈

你的反馈将帮助指导 WinDbg 的开发将前滚。 

- 如果有一项功能，您真正想要查看或执行某困难 bug 等的反馈，请使用反馈中心。

![反馈中心显示反馈选项包括添加新的反馈按钮的屏幕截图](images/windbgx-feedback.png)



## <a name="next-steps"></a>后续步骤

什么是最新版本中的新增功能的信息，请参阅[WinDbg 预览版-What's New](windbg-what-is-new-preview.md)。

查阅这些主题以安装和配置 WinDbg 预览。

- [WinDbg 预览版 – 安装](windbg-install-preview.md)
- [WinDbg Preview – 命令行启动选项](windbg-command-line-preview.md)
- [WinDbg Preview – 设置和工作区](windbg-setup-preview.md)
- [WinDbg Preview – 键盘快捷方式](windbg-keyboard-shortcuts-preview.md)

这些主题描述如何获取连接到你想要调试的环境。 

- [WinDbg 预览 – 启动用户模式会话](windbg-user-mode-preview.md)
- [WinDbg 预览 – 启动内核模式会话](windbg-kernel-mode-preview.md)

这些主题描述一些常见的任务，按菜单选项卡。

- [WinDbg 预览 – 文件菜单](windbg-file-preview.md)
- [WinDbg Preview – 主页菜单](windbg-home-preview.md)
- [WinDbg 预览 – 视图菜单](windbg-view-preview.md)
- [WinDbg Preview – 断点](windbg-breakpoints-preview.md)
- [WinDbg Preview – 数据模型](windbg-data-model-preview.md)
- [WinDbg 预览 – 脚本编写](windbg-scripting-preview.md)


--- 





