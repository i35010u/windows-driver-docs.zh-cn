---
title: 跟踪树窗格中的操作
description: 跟踪树窗格中的操作
ms.assetid: 60ccca37-d264-43dc-a502-3a7c7fe0caef
keywords:
- 静态驱动程序验证工具报表 WDK，跟踪树窗格
- 跟踪树窗格 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3d331239f74ee7ed6fea5fb26fc41d09308ccc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542490"
---
# <a name="trace-tree-pane-actions"></a>跟踪树窗格中的操作

您可以执行以下操作中的**跟踪树**窗格：

- 单步执行跟踪
- 展开和折叠节点

## <a name="step-through-the-trace"></a>单步执行跟踪

单步执行跟踪的最简单方法是通过使用键盘上的箭头键。 下表描述在每个箭头键的操作**跟踪树**窗格。

|键|操作|
|----|----|
|向下键|下移一行的步骤。 此操作将跳过折叠的节点内的代码。|
|向上键|步骤上移一行。 此操作将跳过折叠的节点内的代码。|
|向右键|展开折叠的节点。|
|向左键|折叠展开的节点。|

单步执行中的源代码元素**跟踪树**窗格中，SDV 自动移动光标[源代码窗格](source-code-pane.md)到包含中的元素的源代码行**跟踪树**窗格中，并显示在关联的布尔表达式[状态窗格](state-pane.md)。

## <a name="expand-and-collapse-nodes"></a>展开和折叠节点

使用以下方法之一可展开和折叠中的节点**跟踪树**窗格：

- 若要展开或折叠节点有选择地：
  - 在键盘上，使用箭头键，如前面的表中所述。
  - 单击加号 （+） 展开的节点，或单击减号 （-） 可折叠节点。
- 若要展开或折叠中的节点的所有**跟踪树**窗格中，打开**跟踪树**菜单，然后选择**折叠**（折叠所有节点），**展开**（展开所有节点），或**智能都展开**。 **智能展开**使用启发式方法可展开的源代码的相关元素和折叠的相关性更小的元素。 **智能展开**是默认视图。

> [!NOTE]
> 逐句通过跟踪时，应注意所有折叠的节点。 向下箭头键将跳过的所有代码都是折叠的节点中。
