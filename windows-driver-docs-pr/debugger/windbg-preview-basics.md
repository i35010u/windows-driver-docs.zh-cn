---
title: WinDbg 预览版基础知识
description: 本部分介绍 WinDbg 预览调试器的基本功能。
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 482fc1dacc402dac044e59897c438d4d11f6b74b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216260"
---
# <a name="windbg-preview-basics"></a>WinDbg 预览版基础知识

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png) 

| 标题               | 说明        |
| ------------------- | -------------------|
|[WinDbg 预览版 - 新增功能](./debugging-using-windbg-preview.md)|WinDbg 预览版的新增功能 |

## <a name="the-debugger-data-model"></a>调试器数据模型

| 标题               | 说明        |
| ------------------- | -------------------|
| [dx 命令](./dx--display-visualizer-variables-.md) | 用于显示调试器对象模型表达式的交互式命令 |
| [将 LINQ 与调试器对象配合使用](./using-linq-with-the-debugger-objects.md) | 类似于 SQL 的查询语言 |
| [NatVis 中的本机调试器对象](./native-debugger-objects-in-natvis.md)| 将对象与 NatVis 一起使用 |
| [WinDbg 预览-数据模型](windbg-data-model-preview.md) | 如何在 WinDbg Preview 中使用内置的数据模型支持 |

## <a name="extending-the-data-model"></a>扩展数据模型

| 标题               | 说明        |
| ------------------- | -------------------|
| [JavaScript 调试器脚本](./javascript-debugger-scripting.md) | 如何使用 JavaScript 创建理解调试器对象的脚本  |
| [WinDbg 预览-脚本](./windbg-scripting-preview.md) |使用在脚本中内置的 WinDbg Preview  |
| https://github.com/Microsoft/WinDbg-Samples |调试器团队 GitHub 站点，其中共享最新的 JavaScript (和 c + +) 示例代码。 |
|[JavaScript 扩展中的本机调试器对象](./native-objects-in-javascript-extensions.md) | 介绍如何使用常见对象并提供有关其属性和行为的参考信息。|

## <a name="ttd-basics"></a>TTD 基础知识

| 标题               | 说明        |
| ------------------- | -------------------|
| [时光穿越调试 - 概述](./time-travel-debugging-overview.md) | TTD 概述 |
[时光穿越调试 - 示例应用演练](./time-travel-debugging-walkthrough.md) |  若要进行时间走，请尝试结帐此教程 |

## <a name="ttd-queries"></a>TTD 查询
| 标题               | 说明        |
| ------------------- | -------------------|
| [行程调试对象简介](./time-travel-debugging-object-model.md)。 |您可以使用数据模型来查询时间行程跟踪。  
|  https://github.com/Microsoft/WinDbg-Samples/blob/master/TTDQueries/tutorial-instructions.md |有关如何使用 TTD 查询调试 c + + 代码以查找有问题的代码的教程 |
| https://github.com/Microsoft/WinDbg-Samples/tree/master/TTDQueries/app-sample | 此处提供了实验室中使用的所有代码。

## <a name="videos"></a>视频

观看这些 [碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools) 集，以查看 Windbg 预览的操作。  

| 标题               | 说明        |
|-------------------- |--------------------|
| [碎片整理工具 #182](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-182-WinDbg-Preview-Part-1) |Tim、乍得和的基础知识会超出 WinDbg 预览版和某些功能的基础知识 |
| [碎片整理工具 #183](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-183-WinDbg-Preview-Part-2) | Nick、Tim 和乍得使用 WinDbg 预览版，并浏览快速演示 |
| [碎片整理工具 #184](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-184-JavaScript-in-WinDbg-Preview) | 比尔·盖茨 Andrew 中的脚本功能 |
| [碎片整理工具 #185](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-185-Time-Travel-Debugging-Introduction) | James 和 Ivette 提供时间行程调试简介 |
| [碎片整理工具 #186](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-186-Time-Travel-Debugging-Advanced) | James 和 JCAB 涵盖了高级时间旅行调试 |

## <a name="installation-and-getting-connected"></a>安装和连接 

| 标题               | 说明        |
| ------------------- | -------------------|
| [WinDbg 预览版 - 安装](windbg-install-preview.md) | 安装说明 |
| [WinDbg 预览版 - 启动用户模式会话](windbg-user-mode-preview.md) | 用户模式  |
| [WinDbg 预览版 - 启动内核模式会话](windbg-kernel-mode-preview.md) | 内核模式 |