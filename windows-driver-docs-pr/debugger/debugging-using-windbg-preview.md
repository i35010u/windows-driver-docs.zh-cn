---
title: 使用 WinDbg 预览版进行调试
description: 本部分介绍如何使用 WinDbg 预览调试器执行基本调试任务。
ms.date: 04/03/2019
ms.localizationpriority: High
ms.openlocfilehash: 7d81b172213ebccffd0b126e9ed0432bcbfc9424
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007578"
---
![Windbg 预览版中的小徽标](images/windbgx-preview-logo.png) 

# <a name="debugging-using-windbg-preview"></a>使用 WinDbg 预览版进行调试 

WinDbg 预览版是具有更多新式视觉对象的 WinDbg 全新版本，具有更多新式视觉对象、更快的 windows，以及使用可扩展调试器数据模型前端和中心构建的完整的脚本编写体验。 WinDbg Preview 目前使用与 WinDbg 相同的基础引擎，因此，您使用的所有命令、扩展和工作流仍将像以前一样工作。

有关调试器开发人员团队的最新新闻、提示和技巧，请参阅调试器工具团队博客。
[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)


## <a name="major-features-of-windbg-preview"></a>WinDbg 预览版的主要功能

下面是一些最值得注意的内容，或者是新增功能。

![调试器中的主屏幕](images/windbgx-main-menu.png)


### <a name="general-features"></a>常规功能

- **更轻松的连接设置和重新调用**-WinDbg 预览版包括回调先前会话配置信息的能力。

![调试器中主屏幕的屏幕截图](images/windbgx-start-debugging-menu.png)

- **Easy 反馈渠道**-你的反馈将引导你进行开发工作。 有关详细信息，请参阅[提供反馈](#providing-feedback)

- **转储文件处理器检测**-自动检测处理器体系结构，以便更轻松地进行托管调试。

- **性能改进**现在，Windows 会以异步方式加载和取消操作-当你运行另一个命令时，WinDbg Preview 将停止加载本地、监视或其他窗口。

### <a name="windowing-improvements"></a>窗口化改进

- **反汇编窗口改进**-还改进了 "反汇编" 窗口，当前指令的突出显示在滚动时保持不变。 

    ![调试器中的反汇编窗口](images/windbgx-disassembly.png)


- **内存窗口改进**-"内存" 窗口已突出显示并改善滚动。

- **局部变量和监视数据模型可视化**-"局部变量" 和 "监视" 窗口均基于 dx 命令使用的数据模型。 这意味着 "局部变量" 和 "监视" 窗口将受益于已加载的任何 NatVis 或 JavaScript 扩展，甚至可以支持完整的 LINQ 查询，就像 dx 命令一样。 

- **日志**-此项位于 WinDbg 预览内部的 "记录" 日志中。 可以查看它以进行故障排除或监视长时间运行的进程。 

有关详细信息，请参阅[WinDbg 预览-查看菜单](windbg-view-preview.md)。

- **命令窗口**-使用 "命令" 窗口可以轻松地切换 DML 并清除调试器命令窗口。 所有当前调试器命令都与兼容，并在 WinDbg Preview 中继续工作。


### <a name="dark-theme"></a>深色主题 

使用 "**文件** > "**设置**启用 "深色" 主题。

![显示深色主题的屏幕截图](images/windbgx-dark-theme.png)


### <a name="ribbon-quick-access"></a>功能区快速访问

只需固定最常使用的按钮即可，并折叠功能区以节省屏幕空间。 
 
![显示带有固定项目的 ribon 的屏幕截图](images/windbgx-quick-access.png)



### <a name="source-window"></a>源窗口

已更新源窗口，使其与新式编辑器更多。 

![调试器中脚本菜单的屏幕截图](images/windbgx-source-window.png)


### <a name="highlighting"></a>要点

命令窗口具有两个新的突出显示功能。 选择任何文本将对该文本的任何其他实例突出显示。 然后，可以按 "突出显示/取消突出显示" 或按 Ctrl + Alt + H 来持久保存突出显示内容。 

![显示以黄色突出显示的列的屏幕截图](images/windbgx-highlighting.gif)


### <a name="better-keyboard-navigation"></a>更好的键盘导航

只需按 Ctrl + Tab 即可，只需在 windows 之间导航即可。 

![显示 ctrl 选项卡菜单的屏幕截图](images/windbgx-ctrl-tab.gif)


### <a name="integrated-time-travel-debugging-ttd"></a>集成时间行程调试（TTD）

如果需要对应用程序进行 TTD 跟踪，只需在启动或附加时选中 "带时间的记录过程" 框。 WinDbgNext 会将其设置为 TTD，并在完成记录后打开跟踪。

![显示 ctrl 选项卡菜单的屏幕截图](images/windbgx-ttd.png)

有关详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。


### <a name="debugging-app-packages"></a>调试应用程序包

调试通用应用或后台任务现在是一次单击。

![启动应用包应用程序选项卡，在 "搜索" 框中显示 cal，其中列出了三个应用](images/windbgx-launch-app-package.png)

有关详细信息，请参阅[启动应用程序包](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-user-mode-preview#launch-app-package)。


### <a name="attach-to-a-process"></a>附加到进程

"附加" 对话框的速度更快，更详细，更易于使用。

!["附加到进程" 对话框](images/windbgx-attach-to-a-process-zoomed.png)


### <a name="enhanced-breakpoint-tracking"></a>增强的断点跟踪  

- **启用/禁用断点**-"断点" 窗口显示所有当前断点，并提供对启用和禁用这些断点的轻松访问。 
- **命中计数**-在每次命中断点时，"断点" 窗口将保持运行总计。

有关详细信息，请参阅[断点](windbg-breakpoints-preview.md)。


### <a name="enhanced-data-model-support"></a>增强的数据模型支持

- **内置数据模型支持**-通过内置的数据模型支持来编写 WinDbg 预览版，并通过调试器提供数据模型。
- "**模型" 窗口**-"模型" 窗口提供 "dx" 和 "dx-g" 的可展开和可浏览版本，使你能够在 NatVis、JAVASCRIPT 和 LINQ 查询的基础上创建强大的表。 

有关详细信息，请参阅[WinDbg 预览-数据模型](windbg-data-model-preview.md)。

![调试器中数据模型菜单的屏幕截图](images/windbgx-data-model-menu.png)


### <a name="new-scripting-development-ui"></a>新的脚本开发 UI 

- **脚本开发 UI** -现在提供了一个专门的脚本编写窗口，使开发 JavaScript 和 NatVis 脚本更加容易，并显示错误突出显示和 IntelliSense。

![调试器中脚本菜单的屏幕截图](images/windbgx-scripting-intellisense.png)

有关详细信息，请参阅[WinDbg 预览-脚本](windbg-scripting-preview.md)。

### <a name="backwards-compatibility"></a>向后兼容性 

因为基础调试器引擎是相同的，所以前面的所有调试程序命令和调试器扩展都将继续工作。

## <a name="span-idproviding-feedbackspanproviding-feedback"></a><span id="providing-feedback"></span>提供反馈

你的反馈将有助于进一步指导 WinDbg 的开发。 

- 如果你有一些反馈（如你确实想要查看的功能）或 bug，则请使用反馈中心。

![显示反馈选项（包括 "添加新反馈" 按钮）的反馈中心的屏幕截图](images/windbgx-feedback.png)

## <a name="videos"></a>视频

观看[碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools)的这些剧集显示，以查看 Windbg 预览的操作。  
- [碎片整理工具 #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) -Tim、乍得和的基础知识会超出 WinDbg 预览版和某些功能的基础知识。
- [碎片整理工具 #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) -Nick、Tim 和乍得使用 WinDbg 预览版，并浏览快速演示。
- [碎片整理工具 #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview)帐单和 Andrew 演练 WinDbg 预览版中的脚本功能。
- [碎片整理工具 #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) -James 和 Ivette 提供时间行程调试简介。
- [碎片整理工具 #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) -JAMES 和 JCAB 涵盖了高级时间行程调试。

## <a name="next-steps"></a>后续步骤

有关最新版本中的新增功能的信息，请参阅[WinDbg 预览版-新增功能](windbg-what-is-new-preview.md)。

查看以下主题，以安装和配置 WinDbg Preview。

- [WinDbg 预览版–安装](windbg-install-preview.md)
- [WinDbg 预览–命令行启动选项](windbg-command-line-preview.md)
- [WinDbg 预览–设置和工作区](windbg-setup-preview.md)
- [WinDbg 预览–键盘快捷方式](windbg-keyboard-shortcuts-preview.md)

这些主题介绍如何连接到要调试的环境。 

- [WinDbg 预览版–启动用户模式会话](windbg-user-mode-preview.md)
- [WinDbg 预览版–启动内核模式会话](windbg-kernel-mode-preview.md)

这些主题描述了通过菜单选项卡组织的一些常见任务。

- [WinDbg 预览– "文件" 菜单](windbg-file-preview.md)
- [WinDbg 预览–主页菜单](windbg-home-preview.md)
- [WinDbg 预览– "查看" 菜单](windbg-view-preview.md)
- [WinDbg 预览–断点](windbg-breakpoints-preview.md)
- [WinDbg 预览–数据模型](windbg-data-model-preview.md)
- [WinDbg 预览版–脚本编写](windbg-scripting-preview.md)


--- 





