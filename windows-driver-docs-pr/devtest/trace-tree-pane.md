---
title: 跟踪树窗格
description: 跟踪树窗格
keywords:
- 面板静态驱动程序验证程序
- 静态驱动程序验证器报表 WDK，跟踪树窗格
- 跟踪树窗格 WDK 静态驱动程序验证程序
- 跟踪 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d94af9a80143b0fa82d38b1b1d76a86fcc5db8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815461"
---
# <a name="trace-tree-pane"></a>跟踪树窗格


**跟踪树** 窗格显示对规则冲突路径中执行的源代码关键元素的跟踪，如下面的屏幕截图所示。

!["跟踪树" 窗格的屏幕截图，显示对规则冲突路径中执行的源代码关键元素的跟踪](images/sdv-tracetree.png)

这些关键元素（如函数调用和分配）来自用于检测规则冲突的所有源文件，其中包括 SDV 操作系统模型代码 (SDV 文件) 、SDV 规则源文件 (\* slic) 和驱动程序的源代码中所述。 代码元素按执行顺序显示，即使它们源自不同的文件。

SDV 协调 **跟踪树** 窗格中的显示，并显示在 " [源代码" 窗格](source-code-pane.md) 和 " [状态" 窗格](state-pane.md)中。 单步执行 **跟踪树** 窗格中的源代码时，SDV 会自动突出显示 " **源代码** " 窗格中相应的代码行，并在 " **状态** " 窗格中的相应点显示变量的值。

本节包括：

[了解跟踪树窗格](understanding-the-trace-tree-pane.md)

[跟踪树窗格中的颜色编码](color-coding-in-the-trace-tree-pane.md)

[跟踪树窗格中的操作](trace-tree-pane-actions.md)

 

 





