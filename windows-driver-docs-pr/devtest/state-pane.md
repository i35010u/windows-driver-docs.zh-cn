---
title: 状态窗格
description: 状态窗格
keywords:
- 面板静态驱动程序验证程序
- 静态驱动程序验证器报表 WDK，状态窗格
- 状态窗格 WDK 静态驱动程序验证程序
- 布尔表达式 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78f8a11a276661106fee8c816e6b83ec4c76d86a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826643"
---
# <a name="state-pane"></a>状态窗格


" **状态** " 窗格显示驱动程序、操作系统模型和规则中变量的值的布尔表达式。 SDV 使用这些表达式来构造驱动程序、操作系统模型和规则的抽象，并在验证中使用它们。

以下屏幕截图显示了缺陷查看器中的一个示例 **状态** 窗格。

![缺陷查看器中的 "状态" 窗格的屏幕截图](images/sdv-state.png)

" **状态** " 窗格是缺陷查看器的一个组件。 当在 " [跟踪树" 窗格](trace-tree-pane.md)中突出显示某个代码元素，并在 " [源代码" 窗格](source-code-pane.md)中突出显示相应的源代码行时，" **状态** " 窗格将显示在执行该代码行之前，SDV 为计算结果为 **TRUE** 的驱动程序) 的表达式集中 (的布尔表达式。

### <a name="span-idtracking_boolean_expressionsspanspan-idtracking_boolean_expressionsspantracking-boolean-expressions"></a><span id="tracking_boolean_expressions"></span><span id="TRACKING_BOOLEAN_EXPRESSIONS"></span>跟踪布尔表达式

在验证驱动程序的每个规则时，SDV 将跟踪一组布尔表达式。 " **状态** " 窗格中显示的布尔表达式是该集合中计算结果为 **TRUE** 的表达式。 如果 **跟踪树** 窗格中的元素更改了任何表达式的值，则 " **状态** " 窗格的内容将发生变化，以显示一组计算结果为 **TRUE** 的新表达式。

### <a name="span-idinterpreting_expressions_in_the_state_panespanspan-idinterpreting_expressions_in_the_state_panespaninterpreting-expressions-in-the-state-pane"></a><span id="interpreting_expressions_in_the_state_pane"></span><span id="INTERPRETING_EXPRESSIONS_IN_THE_STATE_PANE"></span>在状态窗格中解释表达式

" **状态** " 窗格中出现的大多数表达式都与规则代码中明显的变量相关。 可以在 "**源代码**" 窗格中的 *RuleName* slic 文件中使用规则 (的源代码，) 帮助您解释表达式。

但是，某些表达式在 " **状态** " 窗格中显示，没有任何可能有助于您解释它们的内部表示形式的详细信息。 例如，

```
x!=x
```

对于 SDV，此表达式表示在跟踪中此点处的此时变量 *x* 的值不等于同一变量在跟踪中的值的情况。 使用驱动程序源代码，规则代码 (的 \* slic) ，并使用 **跟踪树** 窗格中的元素来帮助解释表达式。

### <a name="span-idstep_tabs_in_the_state_panespanspan-idstep_tabs_in_the_state_panespanstep-tabs-in-the-state-pane"></a><span id="step_tabs_in_the_state_pane"></span><span id="STEP_TABS_IN_THE_STATE_PANE"></span>"状态" 窗格中的步骤选项卡

" **状态** " 窗格中的布尔表达式显示在选项卡上。 每个选项卡均通过验证中使用的所有源代码表示跟踪中的一个步骤。 "步骤" 选项卡上的数字表示该步骤在跟踪中的顺序。

通常情况下，因为源代码的每一行只表示跟踪中的一个步骤，所以 " **状态** " 窗格中将只有一个 "步骤" 选项卡。 但是，复杂代码可能会生成多个步骤。

例如，以下屏幕截图显示了包含函数指针的代码行的状态窗格。 在这种情况下，每个 "步骤" 选项卡都表示指针解析的步骤、调用的函数的调用和结果。  ("步骤" 选项卡的数目将显示 SDV 解析函数指针所需的步骤数。 ) 

![显示包含函数指针的代码行的 "状态" 窗格的屏幕截图](images/sdv-statetab.png)

若要按顺序查看 " **状态** " 窗格中的每个 "步骤" 选项卡，请在 " **源代码** " 窗格中选择关联的代码行。 然后，在 " **源代码** " 窗格中重复单击代码行。 每次单击所选的代码行时，SDV 将显示 "下一步" 选项卡，直到您遍历了所有 "步骤" 选项卡。 黄色黄色箭头 (![ 黄色箭头图标，指示所选步骤 ](images/sdv-ico-steptab.png)) 指示选定的步骤。 还可以单击 " **状态** " 窗格中的任何选项卡以查看其内容。

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>条

SDV 经常会跟踪 " **状态** " 窗格中未出现在规则中的表达式，这些表达式似乎与规则直接无关。 这些表达式是通过复杂试探法得出的，SDV 在其尝试关联不同的值和不同规则冲突时使用。 在某些情况下，SDV 无法正确计算表达式。 在这些情况下，SDV 将提供一条消息，指出当前状态未知，并显示该步骤中具有上一已知状态的表达式。 有关说明，请参阅下面的代码示例：

```
Unknown state. Last known state from step 120.
sdv irql current ==2
sdv irql current!=1
sdv irql current!=0
```

 

 





