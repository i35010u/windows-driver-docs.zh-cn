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
- 查找错误 WDK 静态驱动程序验证程序
- 错误 WDK 静态驱动程序验证程序
- 缺陷查看器 WDK 静态驱动程序验证程序
- 中止例程
- 跟踪 WDK 静态驱动程序验证程序
- 规则 WDK 静态驱动程序验证程序
- 面板静态驱动程序验证程序
- 静态驱动程序验证器报表 WDK，窗格
- 静态驱动程序验证器报表 WDK，关于静态驱动程序验证器报表
- 静态驱动程序验证程序 WDK，静态驱动程序验证器报表
- StaticDV WDK，静态驱动程序验证程序报告
- SDV WDK，静态驱动程序验证程序报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2426d159be1a58a2f9eb654bc92475cd138a0d28
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662429"
---
# <a name="using-the-static-driver-verifier-report"></a>使用静态驱动程序验证程序报告


SDV 报表是验证结果的交互式显示。 本部分介绍如何使用 SDV 报表在驱动程序中查找编码错误。 有关报表、windows 的功能以及 windows 中的元素的详细信息，请参阅 [静态驱动程序验证程序报表](static-driver-verifier-report.md)。

### <a name="span-idopen_the_static_driver_verifier_defect_viewerspanspan-idopen_the_static_driver_verifier_defect_viewerspanopen-the-static-driver-verifier-defect-viewer"></a><span id="open_the_static_driver_verifier_defect_viewer"></span><span id="OPEN_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>打开静态驱动程序验证程序缺陷查看器

如果 SDV 在 " **结果** " 窗格中报告了任何 "缺陷" (规则冲突) ，你可以在 "静态驱动程序验证程序" 报表的 " [缺陷查看器](defect-viewer.md) " 窗口中查看冲突中涉及的代码。 "缺陷查看器" 窗口将显示规则冲突的路径中的代码。 每个违反规则都有一个 **缺陷查看器** 窗口 (你一次只能查看一个 **缺陷查看器** 窗口) 。

打开缺陷查看器窗口以获取缺陷：

-   从 " **缺陷 (s) ** " 节点下的列表中选择一个规则 (![ 红色圆圈图标 ](images/sdv-ico-defect.png) ，并在 **结果** 窗格中指示缺陷) ，然后双击规则名称。

此过程仅适用于缺陷。 如果验证结果不是缺陷，如 pass、超时、spaceouts、不适用或其他任何非缺陷结果，SDV 不会生成 **缺陷查看器** 窗口。

以下屏幕截图显示了 "静态驱动程序验证程序" 报表页。

![显示 "静态驱动程序验证程序报表页" 的屏幕截图。](images/sdv-defectviewer.png)

### <a name="span-idreview_the_rulespanspan-idreview_the_rulespanreview-the-rule"></a><span id="review_the_rule"></span><span id="REVIEW_THE_RULE"></span>查看规则

尝试在代码中查找规则冲突之前，请熟悉驱动程序违反的规则。

[静态驱动程序验证程序规则](/windows-hardware/drivers/ddi/index)部分包括一个说明每个规则的主题，例如， [CancelSpinLock](./wdm-cancelspinlock.md)。

若要查看规则的代码，请在 "静态驱动程序验证程序" 报表的 " **源代码** " 窗格中，单击包含规则代码的选项卡，例如 CancelSpinLock. slic。

例如，如果驱动程序按顺序调用[**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))或[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) ，或者驱动程序在释放旋转锁之前退出了例程，则会违反**CancelSpinLock**规则。

### <a name="span-idtrace_the_defect_pathspanspan-idtrace_the_defect_pathspantrace-the-defect-path"></a><span id="trace_the_defect_path"></span><span id="TRACE_THE_DEFECT_PATH"></span>跟踪缺陷路径

当 " **缺陷查看器** " 窗口打开时，" **跟踪树** " 窗格中的元素表示 "缺陷路径" 中的第一个关键驱动程序调用。 在 " **源代码** " 窗格中，以蓝色突出显示源代码的相关行。

下面的屏幕截图显示**静态驱动程序验证程序缺陷查看器**窗口的打开视图，以使 Fail [CancelSpinLock](./wdm-cancelspinlock.md) \_ Driver1 示例驱动程序违反 CancelSpinLock 规则。 在此示例中，CancelSpinLock 规则的冲突路径中的第一个驱动程序调用是对驱动程序的**DispatchSystemControl**例程中的[**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))的调用。

![用于违反 cancelspinlock 规则的静态驱动程序验证程序缺陷查看器窗口的打开视图的屏幕截图](images/sdv-tracetree.png)

### <a name="span-iduse_the_source_code_panespanspan-iduse_the_source_code_panespanuse-the-source-code-pane"></a><span id="use_the_source_code_pane"></span><span id="USE_THE_SOURCE_CODE_PANE"></span>使用 "源代码" 窗格

" [源代码" 窗格](source-code-pane.md) 显示验证中使用的源文件。 如果选择了 " **跟踪树** " 窗格中的某个元素，则与该元素关联的源代码文件将显示在 "相邻 **源代码** " 窗格中文件堆栈的顶部。 若要查看其他源文件，请在 " **源代码** " 窗格中单击源文件的选项卡。

以下屏幕截图显示 "源代码" 窗格。 在此 **源代码** 窗格中，以浅蓝色突出显示的代码行是与 " **跟踪树** " 窗格中所选元素关联的代码行。

!["源代码" 窗格的屏幕截图](images/sdv-sourcecode.png)

驱动程序代码中在缺陷路径中执行的行显示为红色文本。 仅在此示例中，通过查看红色文本行（如第116行和第118行），有时可以看到缺陷，尤其是一个简单的缺陷，如本示例中所使用的。 在这种情况下，驱动程序将获取自旋锁，然后从调度例程返回，而不释放旋转锁定。

### <a name="span-idstep_through_the_tracespanspan-idstep_through_the_tracespanstep-through-the-trace"></a><span id="step_through_the_trace"></span><span id="STEP_THROUGH_THE_TRACE"></span>单步执行跟踪

若要开始跟踪，请在 **跟踪树** 窗格中选择一个元素，然后按向下键。 每次按下箭头时，" **跟踪树** " 窗格中的下一个元素都处于选中状态。

单步执行 **跟踪树** 窗格中的元素时，请在 " **源代码** " 窗格中查看驱动程序代码中的元素。 若要展开代码的折叠部分，请按向右箭头键。 若要折叠展开的代码段，请按向左键。 光标将跳过代码的所有折叠部分。

当您向下滚动 **跟踪树** 窗格中的元素时，所选元素所源自的源代码文件将移动到 **源代码** 窗格中文件堆栈的顶部，并突出显示关联的代码行。

以下屏幕截图显示静态驱动程序验证程序缺陷查看器和跟踪树和源代码窗格。

![静态驱动程序验证程序报表页的屏幕截图](images/sdv-trace1.png)

### <a name="span-iduse_the_rule_file_and_state_panespanspan-iduse_the_rule_file_and_state_panespanuse-the-rule-file-and-state-pane"></a><span id="use_the_rule_file_and_state_pane"></span><span id="USE_THE_RULE_FILE_AND_STATE_PANE"></span>使用 "规则文件和状态" 窗格

您可以使用 " [状态" 窗格](state-pane.md) 查看表示 SDV 在验证期间跟踪的变量值的布尔表达式集。

" **状态** " 窗格中显示的布尔表达式是该集合中计算结果为 **TRUE**的表达式。 如果跟踪树窗格中的元素更改了任何表达式的值，则 " **状态** " 窗格的内容将发生变化，以显示一组计算结果为 **TRUE**的新表达式。

在单步执行 **跟踪树** 窗格时，可以观察 SDV 如何使用这些变量的值来计算 rules (文件中使用的表达式 \*) 。

"静态驱动程序验证程序报表" 页的以下屏幕截图显示了 SDV 测试如何指示驱动程序以前是否获取了自旋锁。 SDV 测试，以查看驱动程序先前是否获取了自旋锁，也就是说，如果 **s** 变量的值为 **1**，则表示已锁定。 在这种情况下， **s！ = 1** (解锁) ，如 " [状态" 窗格](state-pane.md)中所示，SDV 将的值 **设置为** **1**，表示已获取锁。

!["静态驱动程序验证程序" 报表页的屏幕截图，显示 sdv 测试如何指示驱动程序以前是否获取了自旋锁](images/sdv-trace2.png)

### <a name="span-idfind_the_abort_routinespanspan-idfind_the_abort_routinespanfind-the-abort-routine"></a><span id="find_the_abort_routine"></span><span id="FIND_THE_ABORT_ROUTINE"></span>查找中止例程

当驱动程序代码违反规则时，" **跟踪树** " 窗格包含用于报告缺陷的 " **中止** " 例程。

如果缺陷的代码路径较长而复杂，则在 " **跟踪树** " 窗格中向下滚动会很有用，直到找到 " **中止** " 例程，然后使用向上箭头键查找最能立即触发缺陷报告的代码。

例如，如以下屏幕截图中所示，该中止例程与 CancelSpinLock. slic 文件中的某一行相关联，该文件在测试是否获取了该锁 (**s = = locked**) 的情况下报告缺陷。 测试是在调度例程结束时执行的子例程的一部分。 通过此信息，你可以推断驱动程序在从调度例程返回之前未能释放自旋锁。

!["静态驱动程序验证程序" 报表页的屏幕截图，其中显示了中止例程如何与 cancelspinlock. slic 文件中的一行关联](images/sdv-trace3.png)

### <a name="span-idclose_the_static_driver_verifier_defect_viewerspanspan-idclose_the_static_driver_verifier_defect_viewerspanclose-the-static-driver-verifier-defect-viewer"></a><span id="close_the_static_driver_verifier_defect_viewer"></span><span id="CLOSE_THE_STATIC_DRIVER_VERIFIER_DEFECT_VIEWER"></span>关闭静态驱动程序验证程序缺陷查看器

在确定导致缺陷的代码错误后，可以关闭当前规则的 " **静态驱动程序验证程序" 缺陷查看器** 窗口，然后为其他规则打开 **缺陷查看器** 。

若要关闭规则的缺陷查看器：

-   从 " **文件** " 菜单中选择 " **退出**"。

还可以单击 " **关闭** " 按钮 (**X**) 来 **查看缺陷查看器**。 它位于 " **关闭** " 按钮 (**X**) 用于静态驱动程序验证程序报表。

以下屏幕截图显示了如何关闭缺陷查看器。

![显示如何关闭规则的缺陷查看器的屏幕截图](images/sdv-defectviewerclose.png)

 

