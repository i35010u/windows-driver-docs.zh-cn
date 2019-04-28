---
title: 时光穿越调试 - 概述
description: 本部分介绍时间旅行调试。
ms.date: 04/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: f9d25dfef0a29d3d11566e784cdae0257a7183a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349050"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---overview"></a>时光穿越调试 - 概述


## <a name="what-is-time-travel-debugging"></a>什么是时间旅行调试？

时间旅行调试，是一个工具，这样可以记录您的进程运行，请执行，然后更高版本同时向前和向后对其进行重播。 时间旅行调试 (TTD) 可帮助你调试问题更容易通过让你"后退"到调试器会话，而无需重现此问题，直到找到 bug。 
 
TTD，可返回要更好地了解情况导致 bug 和重播多次若要了解如何最大程度来解决该问题的时间。 

TTD 于更具有优势通常缺少促成 ultimate 故障的代码执行的故障转储文件。  

如果您不能找出问题自行，可以与同事共享跟踪和他们可以查看完全什么您正在寻找。 这可允许更轻松协作比实时调试，因为记录的说明是相同的其中的地址位置和执行代码将不同的电脑上不同。 你还可以及时地帮助您的同事共享的特定点找出要启动。 

TTD 有效，并添加降至最低开销捕获跟踪文件中的代码执行的工作。  

TTD 包括一组调试器数据模型对象，以允许你查询使用 LINQ 的跟踪。 例如，可以使用 TTD 对象以查找特定的代码模块加载时或找到的所有异常。 

![示例屏幕截图显示时间的 WinDbg 预览旅行命令和 cdog 应用](images/ttd-windbgx-screen-shot-example-cdog-app.png)

##  <a name="comparison-of-debugging-tools"></a>调试工具的比较

此表总结了可用的各种调试解决方案的优缺点。


|          方法           |                                                      优点                                                       |                                                                                                               缺点                                                                                                                |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       实时调试        |   交互式体验，可以看到执行流，可以更改目标状态，熟悉设置中熟悉的工具。   | 会中断用户体验，可能需要花费精力重复重现此问题，可能会影响安全，不总是生产系统上的选项。  使用重现难以处理返回的点故障以确定原因。 |
|            转储            |                            低的侵入性，无需进行编码前期，基于触发器。                             |                                                          连续快照发布或实时转储提供了简单的"结束时间"视图。 如果未使用，则开销是实质上是零。                                                           |
|      遥测和日志       |            轻型，通常绑定到业务方案 / 用户操作，机器学习友好。             |                                                         （使用任何遥测数据） 的意外的代码路径中出现的问题。 缺少的数据的深度，静态编译的代码。                                                         |
| 调试 (TTD) 按时间顺序查看 | 适合复杂的 bug，将无需进行编码前期成本，友好的可重复脱机调试、 分析捕获的所有内容。 |                                                                 在记录时的较大开销。 可能会收集所需的更多数据。 数据文件会变得大。                                                                 |

## <a name="ttd-availability"></a>TTD 可用性 

从应用商店安装 WinDbg 预览应用程序后可在 Windows 10 上 TTD。  WinDbg 预览版是 WinDbg 的改进的版本与更现代的视觉对象、 更快的 windows、 功能齐全的脚本编写体验，使用内置的可扩展调试器数据模型的支持。 从应用商店下载 WinDbg 预览版的详细信息，请参阅[调试使用 WinDbg 预览版](debugging-using-windbg-preview.md)。

## <a name="administrator-rights-required-to-use-ttd"></a>使用 TTD 所需的管理员权限

若要使用 TTD，您需要运行提升的调试器。 安装使用的帐户具有管理员权限的 WinDbg 预览并记录在调试器中时使用该帐户。 若要运行提升的调试器，右键单击开始菜单中的 WinDbg 预览图标和选择的详细信息 > 以管理员身份运行。

## <a name="video-training"></a>视频培训

若要了解有关 TTD 的详细信息请参阅这些视频。

[碎片整理工具 185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) -Ivette 和 JamesP 超出 TTD 的基础知识和演示 WinDbg 预览版中的某些功能

[碎片整理工具 186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) -Jordi 和 JCAB 演示的 TTD WinDbg 预览版中的多个强大功能

[Cppcon 的谈话 (YouTube)](https://www.youtube.com/watch?v=l1YJTg_A914) -Jordi、 Ken 和 JamesM 按 TTD 显示 WinDbg 在 cppcon 的谈话 2017年预览版


## <a name="trace-file-basics"></a>跟踪文件基础知识 

### <a name="trace-file-size"></a>跟踪文件大小

跟踪文件可获得大并 TTD 用户应确保没有足够的可用空间可用。 如果甚至几分钟后，记录程序，可以快速增长的跟踪文件以达到数千兆字节。 TTD 不会设置跟踪文件以复杂的长时间运行的情况下允许的最大大小。 快速重新创建此问题，将保留跟踪文件大小越小越好。

### <a name="trace-and-index-files"></a>跟踪和索引文件

跟踪 (。运行） 文件存储在录制期间的代码执行。 

录制停止后，索引 (。创建 IDX) 文件以允许更快地访问跟踪信息。 WinDbg 预览打开跟踪文件时，还会自动创建索引文件。

大型、 通常大小的两倍的跟踪文件，也可以是索引文件。  

你可以重新创建从跟踪文件中使用的索引文件 ！ tt.index 命令。

```dbgcmd
0:000> !tt.index
Successfully created the index in 10ms.
```

记录错误和其他记录输出写入 WinDbg 日志文件。

所有输出文件都存储在用户配置的位置。 默认位置是在用户文档文件夹中。 例如，为 User1 TTD 文件将存储在此处：

```console
C:\Users\User1\Documents
```

有关使用跟踪文件的详细信息，请参阅[时间旅行调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)。

## <a name="things-to-look-out-for"></a>需要注意的事项 

### <a name="anti-virus-incompatibilities"></a>防病毒软件不兼容性 

由于 TTD 挂钩到进程来记录它们的方式，可能会遇到不兼容问题。 通常的防病毒软件或尝试跟踪和卷影系统内存调用其他系统软件出现问题。 如果遇到问题的记录，例如没有足够的权限消息，请尝试暂时禁用任何防病毒软件。  

其他的实用程序尝试阻止内存访问，也可能存在问题，例如，Microsoft 增强的缓解体验工具包。 EMET 的详细信息，请参阅[的增强的缓解体验工具包](https://support.microsoft.com/help/2458544/the-enhanced-mitigation-experience-toolkit)。

与 TTD，冲突的环境的另一个示例将 electron 应用程序框架。 在这种情况下可能会记录跟踪，但死锁或进程正在记录的故障，还可以。

### <a name="user-mode-only"></a>仅限用户模式

TTD 目前支持仅用户模式下操作，因此不可能跟踪内核模式过程。 

### <a name="read-only-playback"></a>只读的播放

可以传输返回的时间，但不能更改历史记录。 可以使用读取的内存命令，但不能使用命令修改或写入内存。

### <a name="system-protected-processes"></a>受保护进程的系统

某些 Windows 系统保护的进程，如受保护进程 Light (PPL) 进程受到保护，以便 TTD 不能将自身注入到受保护的进程，以允许执行代码的记录。

### <a name="performance-impact-of-recording"></a>录制的性能影响

记录应用程序或进程会影响性能的 PC。 根据量和录制期间所执行的代码的类型而异的实际性能开销。 您可以预计的 10 个 x-20 x 性能下降普通录制方案中有关。 有时不会明显减慢，但对于更多资源密集型操作 （即文件打开对话框），可以查看录制的影响。

### <a name="trace-file-errors"></a>跟踪文件错误

有某些情况下，跟踪文件可能会发生错误。 有关详细信息，请参阅[调试-故障排除按时间顺序查看](time-travel-debugging-troubleshooting.md)。


## <a name="advanced-features-of-time-travel-debugging"></a>高级的功能的时间旅行调试

下面是一些高级功能，最值得注意 TTD。

### <a name="debugger-data-model-support"></a>调试程序数据模型支持

- **内置数据模型支持**-TTD 包括数据模型支持。 使用 LINQ 查询来分析应用程序故障可以是一个强大的工具。 可以使用 WinDbg 预览版中的数据模型窗口以使用可展开和可浏览版本 dx 和 dx-g，让你创建使用 NatVis、 JavaScript 和 LINQ 查询的表。 

有关调试器的数据模型的常规信息，请参阅[WinDbg 预览版-数据模型](windbg-data-model-preview.md)。 有关使用 TTD 调试器对象模型的信息，请参阅[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)。

### <a name="scripting-support"></a>脚本支持  

- **脚本编写自动化**-脚本支持 JavaScript 和 NatVis 可以自动化地问题调查。 有关详细信息，请参阅[时间旅行调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)。

有关使用 JavaScript 和 NatVis 的常规信息，请参阅[WinDbg 预览版-脚本](windbg-scripting-preview.md)。

### <a name="managed-code-ttd-support"></a>托管的代码 TTD 支持

可以使用 SOS 调试扩展 (sos.dll) 在 64 位模式下运行来调试使用 TTD WinDbg 预览版中的托管的代码。 有关详细信息，请参阅[使用 Windows 调试器调试托管代码](debugging-uwp-apps-using-the-windows-debugger.md)。


## <a name="span-idprovidingfeedbackspanproviding-feedback"></a><span id="providingfeedback"></span>提供反馈

你的反馈将帮助指南时间旅行今后开发优先级。

- 如果有一项功能，您真正想要查看或执行某困难 bug 等的反馈，请使用反馈中心。

![反馈中心显示反馈选项包括添加新的反馈按钮的屏幕截图](images/windbgx-feedback.png)


## <a name="getting-started-with-ttd"></a>开始使用 TTD

查阅这些主题以记录和重播跟踪文件也信息与有关使用跟踪文件和故障排除。

- [时间旅行调试-记录跟踪](time-travel-debugging-record.md)
- [时间旅行调试-重播的跟踪](time-travel-debugging-replay.md)
- [调试-使用跟踪文件按时间顺序查看](time-travel-debugging-trace-file-information.md)
- [时间顺序查看调试-故障排除](time-travel-debugging-troubleshooting.md)
- [时间旅行调试-示例应用程序演练](time-travel-debugging-walkthrough.md)

这些主题描述时间旅行调试中的其他高级的功能。 

- [时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)
- [按照时间顺序逐个调试-JavaScript 自动化](time-travel-debugging-javascript-automation.md)
