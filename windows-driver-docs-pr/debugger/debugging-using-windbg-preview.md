---
title: 使用 WinDbg 预览版进行调试
description: 本部分介绍如何使用 WinDbg 预览版调试程序执行基本的调试任务。
ms.date: 01/16/2020
ms.localizationpriority: High
ms.openlocfilehash: 319542f71ee71f5d3c1913484eab29d752e30fdb
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "76256698"
---
# <a name="debugging-using-windbg-preview"></a>使用 WinDbg 预览版进行调试

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png) 

WinDbg 预览版是 WinDbg 的最新版本，在重要位置构建有可扩展的调试器数据模型，具有更现代的视觉效果、更快速的 Windows 和成熟的脚本体验。 现在，WinDbg 预览版使用与 WinDbg 相同的基础引擎，因此你所习惯的所有命令、扩展和工作流的仍然与以前一样使用。

## <a name="major-features-of-windbg-preview"></a>WinDbg 预览版的主要功能

下面是一些最值得注意的 WinDbg 预览版中已更改的或全新的事项。

![调试程序中的主屏幕](images/windbgx-main-menu.png)

### <a name="general-features"></a>常规功能

- **更轻松的连接设置和重新调用** - WinDbg 预览版包含重新调用以前的会话配置信息的功能。

![调试程序中的主屏幕的屏幕截图](images/windbgx-start-debugging-menu.png)

- **易用的反馈渠道** - 你的反馈将引导我们完成开发工作。 有关详细信息，请参阅[提供反馈](#providing-feedback)

- **转储文件处理器检测** - 自动检测处理器体系结构，以便更轻松地进行托管调试。

- **性能改进** - 窗口现在以异步方式加载并且可以取消 - 运行另一个命令时，WinDbg 预览版会停止加载局部变量窗口、监视窗口或其他窗口。

### <a name="windowing-improvements"></a>窗口化改进

- **反汇编窗口改进** - 反汇编窗口也得到改进。滚动时，突出显示的当前说明保持在原来的位置。

    ![调试程序中的反汇编窗口](images/windbgx-disassembly.png)

- **内存窗口改进** - 内存窗口有突出显示和改进的滚动。

- **局部变量和监视数据模型可视化** - 局部变量窗口和监视窗口都基于 dx 命令使用的数据模型。 这意味着局部变量窗口和监视窗口会受益于已加载的任何 NatVis 或 JavaScript 扩展，甚至可以支持完整的 LINQ 查询，就像 dx 命令一样。

- **日志** - 这是 WinDbg 预览版内部组件的深层次日志。 可以查看它来进行故障排除或监视长时间运行的进程。

有关详细信息，请参阅 [WinDbg 预览版 -“视图”菜单](windbg-view-preview.md)。

- **命令窗口** - 使用命令窗口可以轻松地进行访问，以便切换 DML 和清除调试程序命令窗口。 所有当前的调试程序命令都兼容 WinDbg 预览版，可以继续在其中使用。


### <a name="dark-theme"></a>深色主题 

使用“文件”   >   “设置”来启用深色主题。

![显示深色主题的屏幕截图](images/windbgx-dark-theme.png)

### <a name="ribbon-quick-access"></a>功能区快速访问

直接固定最常用的按钮，可以通过折叠功能区来节省屏幕空间。 

![屏幕截图，显示一个带有固定项的功能区](images/windbgx-quick-access.png)

### <a name="source-window"></a>源代码窗口

源代码窗口已更新，更符合新式编辑器的风格。

![调试程序中的脚本菜单的屏幕截图](images/windbgx-source-window.png)

### <a name="highlighting"></a>突出显示

命令窗口有两项新的突出显示功能。 选择任何文本时，会以巧妙方式突出显示该文本的任何其他实例。 然后，可以按“突出显示/取消突出显示”或 Ctrl+Alt+H 来保持突出显示。

![屏幕截图，显示以黄色突出显示的列](images/windbgx-highlighting.gif)

### <a name="better-keyboard-navigation"></a>更好的键盘导航

直接按 Ctrl+Tab 即可只通过键盘在窗口之间轻松地导航。

![显示 ctrl tab 菜单的屏幕截图](images/windbgx-ctrl-tab.gif)

### <a name="integrated-time-travel-debugging-ttd"></a>集成的时间行程调试 (TTD)

如果需要应用程序的 TTD 跟踪，只需在执行启动或附加操作时勾选“通过时间行程调试来记录”框即可。 WinDbgNext 会针对 TTD 来设置它，并在记录完成后打开跟踪。

![显示 ctrl tab 菜单的屏幕截图](images/windbgx-ttd.png)

有关详细信息，请参阅[时间行程调试 - 概述](time-travel-debugging-overview.md)。

### <a name="debugging-app-packages"></a>调试应用包

现在，只需单击一下即可调试通用应用或后台任务。

![“启动应用包”的“应用程序”选项卡，显示了搜索框中的“cal”，并列出了三个应用](images/windbgx-launch-app-package.png)

有关详细信息，请参阅[启动应用包](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)。

### <a name="attach-to-a-process"></a>附加到进程

附加对话框提供了更多详细信息，包括搜索对话框，更易于使用。

![“附加到进程”对话框](images/windbgx-attach-to-a-process-zoomed.png)

### <a name="enhanced-breakpoint-tracking"></a>增强的断点跟踪  

- **启用/禁用断点** - 断点窗口显示所有当前断点，允许用户轻松地启用和禁用断点。
- **命中计数** - 断点窗口在每次命中断点时都会进行命中次数的汇总。

有关详细信息，请参阅[断点](windbg-breakpoints-preview.md)。

### <a name="enhanced-data-model-support"></a>增强的数据模型支持

- **内置数据模型支持** - 编写的 WinDbg 预览版带有内置数据模型支持，该数据模型在调试程序中自始至终都可以使用。
- **模型窗口** - 模型窗口提供“dx”和“dx -g”的可展开和可浏览版本，用于在 NatVis、JavaScript 和 LINQ 查询的基础上创建功能强大的表。

有关详细信息，请参阅 [WinDbg 预览版 - 数据模型](windbg-data-model-preview.md)。

![调试程序中的数据模型菜单的屏幕截图](images/windbgx-data-model-explore-window.png)

### <a name="new-scripting-development-ui"></a>新的脚本开发 UI

- **脚本开发 UI** - 现在有一个专门构建的脚本窗口，方便 JavaScript 和 NatVis 脚本的开发，可以突出显示错误并带有 IntelliSense 功能。

![调试程序中的脚本菜单的屏幕截图](images/windbgx-scripting-intellisense.png)

有关详细信息，请参阅 [WinDbg 预览版 - 脚本](windbg-scripting-preview.md)。

### <a name="backwards-compatibility"></a>后向兼容性 

由于基础调试程序引擎相同，因此以前的所有调试程序命令和调试程序扩展都可以继续使用。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>提供反馈

你的反馈将引导我们完成 WinDbg 的开发。

- 如果你有反馈（例如，你真的希望看到某项功能，或者你发现一个碍事的 Bug），请使用反馈中心。

![反馈中心的屏幕截图，显示的反馈选项包括“添加新反馈”按钮](images/windbgx-feedback.png)

### <a name="team-blog"></a>团队博客

调试器团队博客虽然现在处于非活动状态，但包含提示和技巧。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)

## <a name="videos"></a>视频

观看有关 [Defrag Tools](https://channel9.msdn.com/Shows/Defrag-Tools)（碎片整理工具）演示的下述视频集，通过实际操作了解 Windbg 预览版。
  
- [Defrag Tools #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1)（碎片整理工具 #182）- Tim、Chad 和 Andy 讲述 WinDbg 预览版的基础知识和部分功能。
- [Defrag Tools #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2)（碎片整理工具 #183）- Nick、Tim 和 Chad 使用 WinDbg 预览版并进行快速演示。
- [Defrag Tools #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview)（碎片整理工具 #184）- Bill 和 Andrew 详细讲述 WinDbg 预览版中的脚本功能。
- [Defrag Tools #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction)（碎片整理工具 #185）- James 和 Ivette 介绍时间行程调试。
- [Defrag Tools #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced)（碎片整理工具 #186）- James 和 JCAB 讲述高级时间行程调试。

## <a name="next-steps"></a>后续步骤

若要了解最新发行版中的新增功能，请参阅 [WinDbg 预览版 - 新增功能](windbg-what-is-new-preview.md)。

请查看以下主题，了解如何安装并配置 WinDbg 预览版。

- [WinDbg 预览版 - 安装](windbg-install-preview.md)
- [WinDbg 预览版 - 命令行启动选项](windbg-command-line-preview.md)
- [WinDbg 预览版 - 设置和工作区](windbg-setup-preview.md)
- [WinDbg 预览版 - 键盘快捷方式](windbg-keyboard-shortcuts-preview.md)

以下主题介绍如何连接到要调试的环境。 

- [WinDbg 预览版 - 启动用户模式会话](windbg-user-mode-preview.md)
- [WinDbg 预览版 - 启动内核模式会话](windbg-kernel-mode-preview.md)

以下主题介绍一些按菜单选项卡组织的常见任务。

- [WinDbg 预览版 - 文件菜单](windbg-file-preview.md)
- [WinDbg 预览版 - 主菜单](windbg-home-preview.md)
- [WinDbg 预览版 - 视图菜单](windbg-view-preview.md)
- [WinDbg 预览版 - 断点](windbg-breakpoints-preview.md)
- [WinDbg 预览版 - 数据模型](windbg-data-model-preview.md)
- [WinDbg 预览版 - 脚本](windbg-scripting-preview.md)
