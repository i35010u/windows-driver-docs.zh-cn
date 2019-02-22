---
title: 使用源代码窗格
description: 使用源代码窗格
ms.assetid: da8d16cd-583f-42b0-857f-64e5103aa379
keywords:
- 静态驱动程序验证工具报表 WDK，源代码窗格
- 源代码窗格 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47019afe6ed0997e368d570f9551106607d59e4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547127"
---
# <a name="using-the-source-code-pane"></a>使用源代码窗格


使用**源代码**窗格以确定每行中的路径规则冲突的代码的来源。

单步执行中的代码元素[跟踪树窗格](trace-tree-pane.md)，在光标**源代码**窗格自动移动到代码中，原始行之间快速切换为所需文件。 若要确定要显示哪些文件，在顶部的选项卡上找到的文件的名称**源代码**窗格中或使用[颜色编码](color-coding-in-the-source-code-pane.md)作为一个视觉提示。

若要确定的验证状态或在跟踪上执行驱动程序源代码的行的效果，请首先单击该行中的代码**源代码**窗格，以便中突出显示该行中的代码元素**跟踪树**窗格。 接下来，使用**跟踪树**窗格中，若要逐步执行的代码行之后，寻找更改中的值时[状态窗格](state-pane.md)。

查找的函数的 SDV 监视规则和识别可能会更改中的值的操作[状态窗格](state-pane.md)，可以读取规则源代码 (*RuleName*.slic) 中的文件**源代码**窗格。

可以使用**源代码**窗格，可以读取任何文件，但游标步骤通过代码逐行; 不执行的顺序。

此外可以将代码复制中的任何选项卡**源代码**窗格和粘贴到支持丰富文本格式 (RTF) 的应用程序文件，例如 Microsoft Word 或写字板。 若要复制的代码，从**编辑**菜单中，选择**全**，然后从**编辑**菜单中，选择**复制**。 或者，按 CTRL + A （选择所有项），然后按 CTRL + C （复制）。

 

 





