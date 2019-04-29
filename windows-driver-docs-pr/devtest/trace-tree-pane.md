---
title: 跟踪树窗格
description: 跟踪树窗格
ms.assetid: 0035e926-7332-45a6-84ea-8c36bc23c61a
keywords:
- 窗格 WDK Static Driver Verifier
- 静态驱动程序验证工具报表 WDK，跟踪树窗格
- 跟踪树窗格 WDK Static Driver Verifier
- 跟踪 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7b768ed2dcd0294ade866b9e5dcf182bb78169
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373147"
---
# <a name="trace-tree-pane"></a>跟踪树窗格


**跟踪树**窗格显示跟踪的规则冲突的路径中执行的源代码的关键元素，如以下屏幕截图中所示。

![跟踪树窗格中显示的规则冲突的路径中执行的源代码的关键元素的跟踪的屏幕截图](images/sdv-tracetree.png)

这些关键元素，如函数调用和赋值，来自所有源文件用来检测规则冲突，其中包括 SDV 操作系统模型代码 （sdv harness.c 文件），SDV 规则源文件 (\*.slic)，并驱动程序的源代码。 代码元素出现，它们执行的顺序，即使它们源自不同的文件。

SDV 坐标中的显示**跟踪树**窗格中显示[源代码窗格](source-code-pane.md)并[状态窗格](state-pane.md)。 单步执行中的源代码**跟踪树**窗格中，SDV 会自动突出显示相应的中的代码行**源代码**，并显示在相应的变量的值中点**状态**窗格。

本部分包括：

[了解跟踪树窗格](understanding-the-trace-tree-pane.md)

[在跟踪树窗格中的颜色编码](color-coding-in-the-trace-tree-pane.md)

[跟踪树窗格中的操作](trace-tree-pane-actions.md)

 

 





