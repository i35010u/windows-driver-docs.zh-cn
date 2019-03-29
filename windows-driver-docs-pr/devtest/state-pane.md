---
title: 状态窗格
description: 状态窗格
ms.assetid: 20fb016e-249b-4d28-9fa8-5d2dd837109f
keywords:
- 窗格 WDK Static Driver Verifier
- 静态驱动程序验证工具报表 WDK，状态窗格
- 状态窗格 WDK Static Driver Verifier
- 布尔表达式 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd6c43db50fb4a9a3c568fc4babcfaf9a021f260
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566497"
---
# <a name="state-pane"></a>状态窗格


**状态**窗格将显示变量的值的布尔表达式中的驱动程序、 操作系统模型和规则。 SDV 使用两个表达式来构造抽象的驱动程序、 操作系统模型和规则，并在验证中使用它们。

下面的屏幕截图显示了一个示例**状态**缺陷查看器中的窗格。

![缺陷查看器中的状态窗格的屏幕截图](images/sdv-state.png)

**状态**窗格是缺陷查看器的组件。 中突出显示的代码元素时[跟踪树窗格](trace-tree-pane.md)，和中突出显示相应的源代码行[源代码窗格](source-code-pane.md)，则**状态**窗格将显示（从 SDV 跟踪驱动程序的表达式集） 的布尔表达式的计算结果为 **，则返回 TRUE**执行的代码行之前。

### <a name="span-idtrackingbooleanexpressionsspanspan-idtrackingbooleanexpressionsspantracking-boolean-expressions"></a><span id="tracking_boolean_expressions"></span><span id="TRACKING_BOOLEAN_EXPRESSIONS"></span>跟踪的布尔表达式

验证驱动程序的每个规则，时 SDV 跟踪一的组布尔表达式。 中显示的布尔表达式**状态**窗格中是表达式的计算结果为该集中**TRUE**。 如果中的元素**跟踪树**窗格将发生变化的内容的任何表达式的值**状态**窗格中更改显示的表达式的计算结果为新的一组**TRUE**.

### <a name="span-idinterpretingexpressionsinthestatepanespanspan-idinterpretingexpressionsinthestatepanespaninterpreting-expressions-in-the-state-pane"></a><span id="interpreting_expressions_in_the_state_pane"></span><span id="INTERPRETING_EXPRESSIONS_IN_THE_STATE_PANE"></span>解释在状态窗格中的表达式

中出现的大多数表达式**状态**窗格与规则代码中都显而易见的变量。 您可以使用源代码的规则 (在*RuleName*.slic 文件中的**源代码**窗格) 可帮助你解释表达式。

但是，某些表达式显示在**状态**而无需任何有关可能会帮助您将其解释其内部表示形式的详细信息窗格。 例如，

```
x!=x
```

SDV，对此表达式表示在其中一个条件变量的值*x*在这种情况在跟踪中不在跟踪中的不同点相同的变量的值相等。 使用此驱动程序源代码，规则代码 (\*.slic)，和中的元素**跟踪树**窗格，以帮助您解释表达式。

### <a name="span-idsteptabsinthestatepanespanspan-idsteptabsinthestatepanespanstep-tabs-in-the-state-pane"></a><span id="step_tabs_in_the_state_pane"></span><span id="STEP_TABS_IN_THE_STATE_PANE"></span>在状态窗格中的步选项卡

中的布尔表达式**状态**选项卡上显示窗格。 每个选项卡表示通过所有验证中使用的源代码在跟踪中的步骤。 在步骤选项卡上的数字表示在跟踪中该步骤的顺序。

通常情况下，由于源代码的每个行表示在跟踪中的只有一个步骤，将只有一个步骤中的选项卡**状态**窗格。 但是，复杂的代码可以生成多个步骤。

例如，下面的屏幕截图显示了状态窗格中显示的包含函数指针的代码行。 在这种情况下，每个步骤的选项卡表示的指针，指向的函数，其结果的调用解析中的步骤。 （步骤选项卡的数目将显示多少步骤花费的 SDV 若要解决的函数指针）。

![状态窗格中显示一行代码，其中包括函数指针的屏幕截图](images/sdv-statetab.png)

若要查看在每个步骤选项卡**状态**窗格中的顺序，选择关联的中的代码行**源代码**窗格。 然后，单击行中的代码**源代码**窗格重复。 每次单击所选的行代码，直到您已完成所有步骤的选项卡关闭并重新打开，SDV 显示下一步的步骤选项卡。 曲线的黄色箭头 (![黄色的曲线的箭头图标，指示所选的步骤](images/sdv-ico-steptab.png)) 指示所选的步骤。 您也可以单击任意选项卡**状态**窗格以查看其内容。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>注释

SDV 通常跟踪中的表达式**状态**窗格中，不会显示在规则中并不直接与该规则会出现。 这些表达式导致复杂试探法，SDV 使用在其尝试将不同的值和不同的规则冲突相关联。 在某些情况下，SDV 无法正确地计算表达式。 在这些情况下，SDV 提供一条消息，表示当前状态为未知的以及显示的最后已知状态的步骤中的表达式。 请参阅下面的代码示例的说明：

```
Unknown state. Last known state from step 120.
sdv irql current ==2
sdv irql current!=1
sdv irql current!=0
```

 

 





