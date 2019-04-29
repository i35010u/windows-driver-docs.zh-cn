---
title: 了解源代码窗格
description: 了解源代码窗格
ms.assetid: 70be3322-fdbc-4d7e-880d-dcbc0fecc39f
keywords:
- 静态驱动程序验证工具报表 WDK，源代码窗格
- 源代码窗格 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520827e10bfaf2f7da109df83e0c1e9d09280194
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351797"
---
# <a name="understanding-the-source-code-pane"></a>了解源代码窗格


**源代码**窗格中显示所有涉及的源代码文件中检测规则冲突，其中包括 SDV 操作系统模型代码 （sdv harness.c 文件），SDV 规则代码 (\*.slic 文件)，并在驱动程序源代码。

下面的屏幕截图显示了一个示例**源代码**窗格。

![缺陷查看器中的源代码窗格的屏幕截图](images/sdv-sourcecode.png)

与不同[跟踪树窗格中](trace-tree-pane.md)，则**源代码**窗格将显示整个文件-不只是执行的代码元素，并显示每个单独的选项卡上的源文件。这种部署使得可以方便地确定在跟踪中的代码元素的源。 中不包含在规则冲突的源代码文件中不会出现**源代码**窗格中，即使它们是在驱动程序源目录中。

SDV 坐标中的显示**源代码**窗格中显示**跟踪树**窗格和[状态窗格](state-pane.md)。 单步执行中的源代码元素**跟踪树**窗格中，SDV 自动突出显示的代码中的一行**源代码**窗格，它包含的元素，并显示在变量的值中的相应点**状态**窗格。

同样，当选择的行*执行*中的代码**源代码**窗格中中的突出显示**跟踪树**窗格移动到相应的操作元素中的代码行。 因为**跟踪树**窗格将显示在您选择的行执行规则冲突的路径中的代码*快进*中的代码**源代码**窗格中，在突出显示**跟踪树**窗格将移动到顶部节点 (*主要*)。

**源代码**窗格是缺陷查看器的组件。

 

 





