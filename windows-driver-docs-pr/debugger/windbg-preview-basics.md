---
title: WinDbg 预览基础知识
description: 本部分介绍 WinDbg 预览调试器的基本功能。
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 98986a36c9094322e60a9f0436182ecbce654217
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866494"
---
![Windbg preview 上的小徽标](images/windbgx-preview-logo.png) 

| 标题               | 描述        |
| ------------------- | -------------------|
|[WinDbg 预览版的新增功能](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview)|新增 WinDbg 预览 |


## <a name="the-debugger-data-model"></a>调试器数据模型

| 标题               | 描述        |
| ------------------- | -------------------|
| [Dx 命令](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) | 交互式命令显示调试器对象模型表达式 |
| [使用 LINQ 与调试器对象](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-linq-with-the-debugger-objects) | SQL 查询语言等 |
| [NatVis 中的本机调试器对象](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-debugger-objects-in-natvis)| NatVis 通过使用对象 |
| [WinDbg 预览版-数据模型](windbg-data-model-preview.md) | 如何使用内置的 WinDbg 预览版中的数据模型支持 |

## <a name="extending-the-data-model"></a>扩展数据模型

| 标题               | 描述        |
| ------------------- | -------------------|
| [JavaScript 调试器脚本](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting) | 如何使用 JavaScript 创建了解调试器对象的脚本  |
| [WinDbg 预览版-脚本](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-scripting-preview) |在脚本中使用 WinDbg 预览生成  |
| https://github.com/Microsoft/WinDbg-Samples |它们在其中共享最新的 JavaScript 调试器团队 GitHub 站点 (和C++) 的示例代码。 |
|[中 JavaScript 扩展本机调试器对象](https://docs.microsoft.com/windows-hardware/drivers/debugger/native-objects-in-javascript-extensions) | 介绍如何使用常见对象和其属性和行为上提供的参考信息。|


## <a name="ttd-basics"></a>TTD 基础知识

| 标题               | 描述        |
| ------------------- | -------------------|
| [按照时间顺序逐个调试-概述](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) | TTD 概述 |
[时间旅行调试-示例应用程序演练](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) |  为提供时间旅行尝试签出此教程 |

## <a name="ttd-queries"></a>TTD 查询
| 标题               | 描述        |
| ------------------- | -------------------|
| [时间旅行调试对象简介](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-object-model)。 |可以使用将数据模型与查询时传输跟踪。  
|  https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md |有关如何调试教程C++代码使用 TTD 查询来查找有问题的代码 |
| https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample | 所有在实验室中使用的代码就可用。

## <a name="videos"></a>视频

观看的这些剧集[碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools)若要了解 Windbg 预览操作。  

| 标题               | 描述        |
|-------------------- |--------------------|
| [碎片整理工具 #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) |Tim，乍得和 Andy 阐述 WinDbg 预览版的基础知识以及的一些功能 |
| [碎片整理工具 #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) | Nick、 Tim 和 Chad 使用 WinDbg 预览和超出的快速演示 |
| [碎片整理工具 #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) | 帐单和 Andrew 逐步完成在 WinDbg 预览版中的脚本撰写功能 |
| [碎片整理工具 #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) | James 和 Ivette 提供和时间的行程调试简介 |
| [碎片整理工具 #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) | James 和 JCAB 包括高级的调试时间旅行 |

## <a name="installation-and-getting-connected"></a>安装和进行连接 

| 标题               | 描述        |
| ------------------- | -------------------|
| [WinDbg 预览版 – 安装](windbg-install-preview.md) | 安装说明 |
| [WinDbg 预览 – 启动用户模式会话](windbg-user-mode-preview.md) | 用户模式  |
| [WinDbg 预览 – 启动内核模式会话](windbg-kernel-mode-preview.md) | 内核模式 |
