---
title: 使用静态驱动程序验证程序报告
description: 使用静态驱动程序验证程序报告
ms.assetid: ca6eaa53-cee5-4caf-b1e1-035ea800779b
keywords:
- 静态驱动程序验证程序 WDK，验证结果
- StaticDV WDK，验证结果
- SDV WDK，验证结果
- 静态驱动程序验证程序 WDK，查找错误
- StaticDV WDK，查找错误
- SDV WDK，查找错误
- 查找错误 WDK Static Driver Verifier
- 错误 WDK Static Driver Verifier
- 缺陷的查看器 WDK Static Driver Verifier
- 中止例程
- 跟踪 WDK Static Driver Verifier
- 规则 WDK Static Driver Verifier
- 窗格 WDK Static Driver Verifier
- 静态驱动程序验证工具报表 WDK 窗格
- Static Driver Verifier 报表 WDK，关于 Static Driver Verifier 报表
- Static Driver Verifier WDK、 Static Driver Verifier 报表
- StaticDV WDK、 Static Driver Verifier 报表
- SDV WDK、 Static Driver Verifier 报表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cc0afed9f938254957b4cd9d8c08a83e6102158
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327273"
---
# <a name="using-the-static-driver-verifier-report"></a>使用静态驱动程序验证程序报告


SDV 报表是以交互方式显示的验证结果。 本部分介绍如何使用 SDV 报表要在驱动程序中查找编码错误。 有关报表的详细信息，windows 和 windows 中的元素的功能，请参阅[静态驱动程序验证工具报告](static-driver-verifier-report.md)。

### <a name="span-idopenthestaticdriververifierdefectviewerspanspan-idopenthestaticdriververifierdefectviewerspanopen-the-static-driver-verifier-defect-viewer"></a><span id="open_the_static_driver_verifier_defect_viewer"></span><span id="OPEN_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>打开的 Static Driver Verifier 缺陷查看器

如果 SDV 中报告任何"缺陷"（规则冲突）**结果**窗格中，您可以查看在冲突中涉及的代码[缺陷查看器](defect-viewer.md)静态驱动程序验证工具报告的窗口。 缺陷查看器窗口显示规则冲突的路径中的代码。 还有一个**缺陷查看器**违反了每个规则的窗口 (您可以查看只有一个**缺陷查看器**窗口一次)。

若要打开一个缺陷脱离查看器窗口：

-   从下的列表中选择的规则**Defect(s)** 节点 (![带有白色 x，该值指示有缺陷的红色圆圈图标](images/sdv-ico-defect.png)) 中**结果**窗格中，然后双击规则名称。

此过程仅适用于缺陷。 SDV 不会生成**脱离查看器**窗口，如果验证的结果不是缺陷，例如阶段、 超时、 spaceouts，不适用或任何其他非缺陷结果。

下面的屏幕截图显示了静态驱动程序验证工具报表页。

![静态驱动程序验证工具报表页面的屏幕截图](images/sdv-defectviewer.png)

### <a name="span-idreviewtherulespanspan-idreviewtherulespanreview-the-rule"></a><span id="review_the_rule"></span><span id="REVIEW_THE_RULE"></span>查看规则

尝试查找之前在代码中，规则冲突熟悉该驱动程序违反的规则。

[驱动程序验证程序的静态规则](https://msdn.microsoft.com/library/windows/hardware/ff551714)部分包括本主题介绍每个规则，例如， [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)。

若要查看在该规则的代码**源代码**窗格中的静态驱动程序验证器报表，单击与规则中的代码，例如 CancelSpinLock.slic 选项卡。

例如， **CancelSpinLock**如果驱动程序调用违反规则[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)或者[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)不按顺序，或如果该驱动程序释放自旋锁前退出例程。

### <a name="span-idtracethedefectpathspanspan-idtracethedefectpathspantrace-the-defect-path"></a><span id="trace_the_defect_path"></span><span id="TRACE_THE_DEFECT_PATH"></span>跟踪缺陷路径

当**脱离查看器**窗口将打开中的元素**跟踪树**表示缺陷路径中的第一个必需的驱动程序调用的窗格中选择。 在中**源代码**窗格中，关联的源代码行突出显示为蓝色。

以下屏幕截图显示打开的视图**静态驱动程序验证程序缺陷查看器**窗口中的冲突[CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)由失败的规则\_Driver1 示例驱动程序。 在此示例中，第一个驱动程序调用路径中发生 CancelSpinLock 规则的冲突是调用[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)中的驱动程序**DispatchSystemControl**例程。

![打开的 static driver verifier 的视图的屏幕截图脱离 cancelspinlock 规则的冲突查看器窗口](images/sdv-tracetree.png)

### <a name="span-idusethesourcecodepanespanspan-idusethesourcecodepanespanuse-the-source-code-pane"></a><span id="use_the_source_code_pane"></span><span id="USE_THE_SOURCE_CODE_PANE"></span>使用源代码窗格

[源代码窗格](source-code-pane.md)显示在验证中使用的源文件。 元素位于**跟踪树**窗格中选择，与元素关联的源的代码文件将显示在相邻文件堆栈顶部**源代码**窗格。 若要查看不同的源代码文件，单击对应的选项卡中的源文件**源代码**窗格。

下面的屏幕截图显示了源代码窗格。 在此**源代码**窗格中，将以浅蓝色突出显示的代码行是那些与中的所选元素相关联**跟踪树**窗格。

![源的代码窗格的屏幕截图](images/sdv-sourcecode.png)

以红色文本显示驱动程序代码中的缺陷的路径中执行的行。 通过只查看行的红色文本，如行 116 和 118 在此示例中，有时可以看到缺陷，尤其是在此示例中使用的类似的简单缺陷。 在这种情况下，驱动程序获取数值调节钮锁，，然后从调度例程返回而不释放自旋锁。

### <a name="span-idstepthroughthetracespanspan-idstepthroughthetracespanstep-through-the-trace"></a><span id="step_through_the_trace"></span><span id="STEP_THROUGH_THE_TRACE"></span>单步执行跟踪

若要开始跟踪，请选择中的元素**跟踪树**窗格中，然后再按向下箭头键。 每次按向下箭头中的下一个元素**跟踪树**窗格中选择。

单步执行中的元素**跟踪树**窗格中，观看**源代码**窗格中的驱动程序代码中的元素。 若要展开折叠的代码段，按右箭头键。 若要折叠展开的代码部分，按向左箭头键。 光标将跳过所有已折叠的代码段。

向下滚动查看中的元素**跟踪树**窗格中，所选的元素出自移动到文件中的堆栈顶部的源代码文件**源代码**窗格和关联突出显示的代码行。

下面的屏幕截图显示了具有跟踪树和源代码窗格静态驱动程序验证程序缺陷查看器。

![静态驱动程序验证工具报表页面的屏幕截图](images/sdv-trace1.png)

### <a name="span-idusetherulefileandstatepanespanspan-idusetherulefileandstatepanespanuse-the-rule-file-and-state-pane"></a><span id="use_the_rule_file_and_state_pane"></span><span id="USE_THE_RULE_FILE_AND_STATE_PANE"></span>使用规则文件和状态窗格

可以使用[状态窗格](state-pane.md)若要查看表示在验证期间跟踪 SDV 的变量的值的布尔表达式的集合。

中显示的布尔表达式**状态**窗格中是表达式的计算结果为该集中**TRUE**。 如果在跟踪树窗格中的元素的内容的任何表达式的值更改**状态**窗格中更改显示的表达式的计算结果为新的一组**TRUE**。

当通过单步**跟踪树**窗格中，您可以观察 SDV 如何使用这些变量的值来计算规则文件中使用的表达式 (\*.slic)。

SDV 测试如何指示是否驱动程序以前获取旋转锁静态驱动程序验证工具报表页显示以下屏幕截图。 SDV 测试以查看是否驱动程序以前获取旋转锁，也就是说，如果的值**s**变量是**1**，锁定的含义。 在这种情况下， **s ！ = 1** （已解除锁定） 中, 所示[状态窗格](state-pane.md)，因此 SDV 设置的值**s**到**1**，指示的锁，获取。

![显示如何 sdv 测试静态驱动程序验证工具报表页面的屏幕截图指示是否驱动程序以前获取旋转锁](images/sdv-trace2.png)

### <a name="span-idfindtheabortroutinespanspan-idfindtheabortroutinespanfind-the-abort-routine"></a><span id="find_the_abort_routine"></span><span id="FIND_THE_ABORT_ROUTINE"></span>查找中止例程

当驱动程序代码违反规则时**跟踪树**窗格中包含**中止**例程用于报告缺陷。

长而复杂的代码路径与缺陷时，通常很有用来向下滚动**跟踪树**窗格中，直到找到**中止**例程，，然后使用向上键查找的代码，大多数立即触发缺陷报告。

例如，以下屏幕截图中所示，中止例程是与报告测试是否已获取锁后的缺陷 CancelSpinLock.slic 文件中的一行相关联 (**s = = 锁定**)。 测试是子例程的调度例程结束时执行的一部分。 中的信息，您可以推断出该驱动程序无法从调度例程返回前释放自旋锁。

![显示了如何中止例程与 cancelspinlock.slic 文件中的一行相关联的静态驱动程序验证工具报表页面的屏幕截图](images/sdv-trace3.png)

### <a name="span-idclosethestaticdriververifierdefectviewerspanspan-idclosethestaticdriververifierdefectviewerspanclose-the-static-driver-verifier-defect-viewer"></a><span id="close_the_static_driver_verifier_defect_viewer"></span><span id="CLOSE_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>关闭 Static Driver Verifier 缺陷查看器

确定导致缺陷的代码错误之后，你可以关闭**静态驱动程序验证程序脱离 Viewer**窗口当前的规则，然后打开**脱离查看器**不同规则。

若要关闭缺陷查看器的规则：

-   从**文件**菜单中，选择**退出**。

此外可以单击**关闭**按钮 (**X**) 的**缺陷查看器**。 它位于正下方**关闭**按钮 (**X**) 为静态的驱动程序验证工具报表。

以下屏幕截图演示了如何关闭缺陷查看器。

![显示如何关闭一个规则的缺陷查看器的屏幕截图](images/sdv-defectviewerclose.png)

 

 





