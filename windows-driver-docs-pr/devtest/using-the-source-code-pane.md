---
title: 使用源代码窗格
description: 使用源代码窗格
keywords:
- 静态驱动程序验证器报表 WDK，源代码窗格
- 源代码窗格 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb1556aabb21eff7e4a7597a33c5610d8783ef34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826659"
---
# <a name="using-the-source-code-pane"></a>使用源代码窗格


使用 " **源代码** " 窗格确定规则冲突路径中的每行代码的来源。

单步执行 [跟踪树窗格](trace-tree-pane.md)中的代码元素时，" **源代码** " 窗格中的光标会自动移至原始代码行，并在必要时在文件之间快速切换。 若要确定正在显示的文件，请在 " **源代码** " 窗格的最顶层选项卡中查找文件名，或使用 [颜色编码](color-coding-in-the-source-code-pane.md) 作为视觉提示。

若要确定执行的驱动程序源代码在验证或跟踪状态下的效果，请首先单击 " **源代码** " 窗格中的代码行，以便在 " **跟踪树** " 窗格中突出显示该行中的代码元素。 接下来，使用 **跟踪树** 窗格遍历其后的代码行，同时观察 [状态窗格](state-pane.md)中的更改值。

若要查找 SDV 为该规则监视的函数并确定可能更改 "[状态" 窗格](state-pane.md)中的值的操作，可以在 "**源代码**" 窗格中 (*RuleName*) 文件中读取规则源代码。

您可以使用 " **源代码** " 窗格读取任何文件，但游标逐行执行代码，不在执行顺序中。

你还可以从 " **源代码** " 窗格的任何选项卡复制代码，并将其粘贴到支持 rtf) 文件（如 Microsoft Word 或写字板） (rtf 格式的应用程序。 若要复制代码，请从 " **编辑** " 菜单中选择 "全 **选** "，然后从 " **编辑** " 菜单中选择 " **复制**"。 或者按 CTRL + A (选择所有) 然后按 CTRL + C (复制) 。

 

 





