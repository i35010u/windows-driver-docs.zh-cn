---
title: 时光穿越调试 - 概述
description: 本部分介绍了时间行程调试。
ms.date: 01/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3ef357d348ba9cf86f84480ff6c675195c09da77
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802707"
---
# <a name="time-travel-debugging---overview"></a>时光穿越调试 - 概述

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png) 

## <a name="what-is-time-travel-debugging"></a>什么是旅行调试？

时间行程调试是一种工具，可让你记录正在运行的进程的执行，然后在以后向前和向后重播。使用行程调试 (TTD) 可以通过使你 "后退" 调试器会话来更轻松地调试问题，而无需在发现 bug 之前重现问题。 

TTD 可让你返回时间，以便更好地了解导致错误的条件并多次重播，以了解如何最好地解决问题。 

与故障转储文件相比，TTD 具有更多优点，这通常会导致最终失败导致的代码执行。  

如果您不能自行判断问题所在，您可以与同事共享跟踪，并且可以确切地查看您正在查看的内容。 与实时调试相比，此操作可以更方便地进行协作，因为记录的说明是相同的，其中的地址位置和代码执行在不同的 Pc 上将有所不同。 你还可以共享特定的时间点，以帮助你的同事找出开始位置。

TTD 的效率更高，可在跟踪文件中捕获代码执行时尽可能少地添加开销。  

TTD 包含一组调试器数据模型对象，使你可以使用 LINQ 查询跟踪。 例如，你可以使用 TTD 对象来查找特定代码模块的加载时间或查找所有异常。

![显示时间行程命令和三个时间线的 WinDbg preview 的示例屏幕截图](images/ttd-windbgx-screen-shot-example.png)

## <a name="comparison-of-debugging-tools"></a>调试工具的比较

下表总结了可用的各种调试解决方案的优点和缺点。

|          方法           |                                                      优点                                                       |                                                                                                               缺点                                                                                                                |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       实时调试        |   交互式体验，查看执行流，可以更改目标状态（熟悉的工具）。   | 中断用户体验后，可能需要精力重复重现该问题，这可能会影响安全性，而不是始终是生产系统上的一个选项。  从故障点重新开始，难以确定原因。 |
|            转储            |                            根据触发器，无需预先编码，侵入性。                             |                                                          连续的快照或实时转储提供简单的 "一段时间" 视图。 如果未使用，则开销实质上是零。                                                           |
|      遥测 & 日志       |            轻型，通常绑定到业务方案/用户操作、机器学习友好。             |                                                         不 (遥测) 的意外代码路径中会出现问题。 缺少数据深度，静态编译到代码中。                                                         |
| 行程调试 (TTD)  | 非常复杂的 bug，无需预先编码、脱机的可重复调试、可识别分析、捕获一切内容。 |                                                                 记录时间大的开销。 可能会收集需要的更多数据。 数据文件可能会变得很大。                                                                 |

## <a name="ttd-availability"></a>TTD 可用性 

从应用商店安装 WinDbg Preview 应用后，TTD 在 Windows 10 上可用。  WinDbg 预览版是具有更多新式视觉对象、更快的 windows、具有完备功能的脚本编写体验的 WinDbg 的改进版本，并内置了对可扩展调试器数据模型的支持。 有关从应用商店下载 WinDbg Preview 的详细信息，请参阅 [使用 WinDbg preview 进行调试](debugging-using-windbg-preview.md)。

## <a name="administrator-rights-required-to-use-ttd"></a>使用 TTD 所需的管理员权限

若要使用 TTD，需要运行提升的调试器。 使用具有管理员权限的帐户安装 WinDbg 预览版，并在调试器中记录时使用该帐户。 若要以提升的权限运行调试器，请选择并按住 (或右键单击 "开始" 菜单中的 "WinDbg 预览" 图标) ，然后选择 "更多 > 以管理员身份运行"。

## <a name="video-training"></a>视频培训

若要了解有关 TTD 的详细信息，请参阅这些视频。

[碎片整理工具 185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) -Ivette 和 JamesP 介绍了 TTD 的基本知识，并演示了 WinDbg 预览版中的一些功能

[碎片整理工具 186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) -在 WinDbg 预览版中，JORDI 和 JCAB 演示更好的 TTD 功能

[CppCon (YouTube) ](https://www.youtube.com/watch?v=l1YJTg_A914) -Jordi，Ken 和 JamesM 在 WinDbg Preview 的 CppCon 2017

## <a name="trace-file-basics"></a>跟踪文件基础知识

### <a name="trace-file-size"></a>跟踪文件大小

跟踪文件可能会很大，TTD 的用户需要确保有足够的可用空间。 如果录制节目甚至几分钟，跟踪文件就会迅速增长到数 gb。 TTD 不会将跟踪文件的最大大小设置为允许复杂长时间运行的方案。 快速重新创建问题，会使跟踪文件的大小尽可能小。

### <a name="trace-and-index-files"></a>跟踪和索引文件

跟踪 (。运行) 文件存储在记录过程中执行的代码。 

停止记录后，索引 (。创建 IDX) 文件，以便更快地访问跟踪信息。 当 WinDbg Preview 打开跟踪文件时，也会自动创建索引文件。

索引文件也可以是大，通常是跟踪文件的两倍。  

您可以使用！ tt 命令重新创建跟踪文件中的索引文件。

```dbgcmd
0:000> !tt.index
Successfully created the index in 10ms.
```

记录错误和其他记录输出会写入到 WinDbg 日志文件。

所有输出文件都存储在用户配置的位置中。 默认位置在 "用户" 文档文件夹中。 例如，对于 User1，将在此处存储 TTD 文件：

```console
C:\Users\User1\Documents
```

有关使用跟踪文件的详细信息，请参阅 [行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)。

## <a name="things-to-look-out-for"></a>要查看的项

### <a name="anti-virus-incompatibilities"></a>防病毒不兼容

你可能会遇到不兼容问题，因为 TTD 挂钩如何处理它们。 出现防病毒或其他系统软件（尝试跟踪和隐藏系统内存调用）时，通常会出现问题。 如果遇到记录问题（如权限不足），请尝试暂时禁用任何防病毒软件。  

尝试阻止内存访问的其他实用程序也可能有问题，例如，Microsoft 增强的缓解体验工具包。 有关 EMET 的详细信息，请参阅 [增强的缓解体验工具包](https://support.microsoft.com/help/2458544/the-enhanced-mitigation-experience-toolkit)。

与 TTD 冲突的环境的另一个示例是 electron 应用程序框架。 在这种情况下，跟踪可能会记录，但也可能会导致正在记录的进程发生死锁或故障。

### <a name="user-mode-only"></a>仅用户模式

TTD 目前仅支持用户模式操作，因此无法跟踪内核模式进程。 

### <a name="read-only-playback"></a>只读播放

您可以及时返回，但不能更改历史记录。 您可以使用 "读取内存" 命令，但不能使用修改或写入内存的命令。

### <a name="system-protected-processes"></a>系统保护的进程

某些 Windows 系统保护的进程（例如受保护的进程 (PPL) 进程）受到保护，因此 TTD 不能将其自身注入到受保护的进程中以允许执行代码的记录。

### <a name="performance-impact-of-recording"></a>记录对性能的影响

记录应用程序或进程会影响计算机的性能。 实际的性能开销因记录期间要执行的代码的数量和类型的不同而异。 在典型的录制方案中，可能会对性能造成20倍的影响。 有时，不会有明显的减速，但需要更多的资源密集型操作 (即 "文件打开" 对话框) 您可以看到记录的影响。

### <a name="trace-file-errors"></a>跟踪文件错误

在某些情况下，可能会发生跟踪文件错误。 有关详细信息，请参阅 [行程调试-故障排除](time-travel-debugging-troubleshooting.md)。

## <a name="advanced-features-of-time-travel-debugging"></a>行程调试的高级功能

下面是一些最值得注意的 TTD 高级功能。

### <a name="timelines"></a>时间线

时间线是执行过程中发生的事件的直观表示形式。 这些事件可以是以下位置：断点、内存读取/写入、函数调用和返回以及异常。 有关时间线的详细信息，请参阅 [WinDbg 预览-时间线](windbg-timeline-preview.md)。

### <a name="debugger-data-model-support"></a>调试器数据模型支持

- **内置的数据模型支持** -TTD 包括数据模型支持。 使用 LINQ 查询分析应用程序故障可能是一个功能强大的工具。 您可以使用 WinDbg Preview 中的 "数据模型" 窗口处理 "dx" 和 "dx-g" 的可展开和可浏览版本，使您可以使用 NatVis、JavaScript 和 LINQ 查询创建表。

有关调试器数据模型的常规信息，请参阅 [WinDbg 预览-数据模型](windbg-data-model-preview.md)。 有关使用 TTD 调试器对象模型的信息，请参阅 [行程调试-时间行程调试对象简介](time-travel-debugging-object-model.md)。

### <a name="scripting-support"></a>脚本支持  

- **脚本编写自动化** -针对 JavaScript 和 NatVis 的脚本支持可让问题调查实现自动化。 有关详细信息，请参阅 [时间行程调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)。

有关使用 JavaScript 和 NatVis 的常规信息，请参阅 [WinDbg 预览-脚本](windbg-scripting-preview.md)。

### <a name="managed-code-ttd-support"></a>托管代码 TTD 支持

可以使用 "SOS 调试扩展" ( 在64位模式下运行的 # A0) 在 WinDbg Preview 中使用 TTD 调试托管代码。 有关详细信息，请参阅 [使用 Windows 调试器调试托管代码](debugging-uwp-apps-using-the-windows-debugger.md)。

## <a name="span-idprovidingfeedbackspanproviding-feedback"></a><span id="providingfeedback"></span>提供反馈

你的反馈将有助于指导发展行程发展的优先级。

- 如果你有反馈（例如，你真的希望看到某项功能，或者你发现一个碍事的 Bug），请使用反馈中心。

![反馈中心的屏幕截图，显示的反馈选项包括“添加新反馈”按钮](images/windbgx-feedback.png)


## <a name="getting-started-with-ttd"></a>TTD 入门

有关使用跟踪文件和故障排除的详细信息，请参阅这些主题：记录和重播跟踪文件以及有关使用跟踪文件和疑难解答的信息。

- [时间旅行调试 - 记录跟踪](time-travel-debugging-record.md)
- [时光穿越调试 - 重放跟踪](time-travel-debugging-replay.md)
- [时光穿越调试 - 使用跟踪文件](time-travel-debugging-trace-file-information.md)
- [时光穿越调试 - 故障排除](time-travel-debugging-troubleshooting.md)
- [时光穿越调试 - 示例应用演练](time-travel-debugging-walkthrough.md)

这些主题介绍了时间旅行调试的其他高级功能。 

- [时光穿越调试 - 时光穿越调试对象简介](time-travel-debugging-object-model.md)
- [时光穿越调试 - JavaScript 自动化](time-travel-debugging-javascript-automation.md)
