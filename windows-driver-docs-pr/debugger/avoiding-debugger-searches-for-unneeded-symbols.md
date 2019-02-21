---
title: 避免调试器搜索不需要的符号
description: 为何符号加载有时需要花费很长时间？ 这取决于符号名称是否是限定或未限定。
ms.assetid: 710BAEAF-BC45-416E-8359-69E9DFCA2570
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2ac691b1bb58f52f506e9fb7d3fbf6caa5031fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542715"
---
# <a name="avoiding-debugger-searches-for-un-needed-symbols"></a>避免调试器搜索不需要的符号


**上次更新时间：**

-   2007 年 5 月 27日日

调试您的驱动程序，仅具有很长时间的调试器暂停时它会尝试加载符号的驱动程序，不属于你，甚至无关紧要的手头的调试任务时到达有趣的断点。 这是怎么回事？

默认情况下，为在需要符号由调试器中加载。 （这称为延迟的符号加载或延迟加载的符号。）每当执行符号显示调用命令时，调试器查找符号。 如果已设置监视变量无效，无法在当前上下文中，例如函数参数或局部变量的不存在于当前堆栈帧，因为它们会变得无效的上下文更改时，这可能发生在断点处。 它还可能如果只需键入错误的符号名或执行命令的使用无效的调试器调试器启动寻找匹配的符号。

为什么这有时需要太长？ 这取决于符号名称是否是限定或未限定。 限定的符号名称前面带有包含的符号的模块的名称-例如，myModule ！ myVar。 非限定的符号名称未指定的模块名称-例如，myOtherVar。

在限定名称的情况下调试器查找中指定的模块的符号并，如果未加载的模块，将加载模块 （假设该模块存在并且包含的符号）。 这种情况相当快的速度。

在非限定名称的情况下调试器不"知道"的模块包含的符号，因此它必须在所有这些看起来。 调试器首先会检查所有已加载的模块符号，然后，如果它不能匹配任何加载的模块中的符号，调试器会继续其搜索条件加载所有已卸载的模块，下游应用商店的开始和结尾符号服务器，如果你是使用其中一个。 显然，这可能需要很多时间。

## <a name="span-idhowtopreventautomaticloadingforunqualifiedsymbolsspanspan-idhowtopreventautomaticloadingforunqualifiedsymbolsspanspan-idhowtopreventautomaticloadingforunqualifiedsymbolsspanhow-to-prevent-automatic-loading-for-unqualified-symbols"></a><span id="How_to_prevent_automatic_loading_for_unqualified_symbols_"></span><span id="how_to_prevent_automatic_loading_for_unqualified_symbols_"></span><span id="HOW_TO_PREVENT_AUTOMATIC_LOADING_FOR_UNQUALIFIED_SYMBOLS_"></span>如何阻止自动加载的非限定的符号


**SYMOPT\_否\_UNQUALIFIED\_加载**选项禁用或启用调试器自动加载模块时它会搜索的非限定的符号。 当**SYMOPT\_否\_UNQUALIFIED\_加载**是组和调试器尝试匹配的非限定的符号，它将搜索唯一模块，已被加载，并会停止搜索时它不能与匹配的符号，而不是加载已卸载的模块，以继续搜索。 此选项不会影响搜索限定名称。

**SYMOPT\_否\_UNQUALIFIED\_加载**默认情况下处于关闭状态。 若要激活此选项，请使用 **-snul**命令行选项，或运行调试器时，使用 **.symopt + 0x100**或 **.symopt 0x100**打开或关闭，关闭此选项分别。

若要查看的效果**SYMOPT\_否\_UNQUALIFIED\_加载**，尝试此实验：

1.  激活干扰符号加载 (**SYMOPT\_调试**) 通过使用 **-n**命令行选项，或如果调试器已在运行，使用 **.symopt + 0x80000000**或 **！ 符号干扰**调试器扩展命令。 **SYMOPT\_调试**指示调试器在加载它时显示其搜索符号，如每个模块的名称有关的信息或一条错误消息，如果调试器无法找到的文件。
2.  指示调试程序评估不存在的符号 (例如，键入 **？ asdasdasd**)。 调试器应报告大量错误，而它会搜索不存在的符号。
3.  激活**SYMOPT\_否\_UNQUALIFIED\_加载**通过 **.symopt + 0x100**。
4.  重复步骤 2。 调试器应搜索不存在的符号，仅加载的模块，它应完成的任务要快得多。
5.  若要禁用**SYMOPT\_调试**，使用 **.symopt 0x80000000**或 **！ 符号静默**调试器扩展命令。

有多种选项都是可用来控制调试器如何加载和使用的符号。 符号选项以及如何使用它们的完整列表，请参阅联机文档提供有关 Windows 调试工具中的"设置符号选项"。 最新版本的 Windows 调试工具包是可作为从 web 免费下载，或可以从 Windows DDK、 Platform SDK 或客户支持诊断 CD 中安装包。

## <a name="span-idwhatshouldyoudospanspan-idwhatshouldyoudospanspan-idwhatshouldyoudospanwhat-should-you-do"></a><span id="What_should_you_do__"></span><span id="what_should_you_do__"></span><span id="WHAT_SHOULD_YOU_DO__"></span>您该怎么办？


-   若要加快搜索符号，请使用断点和只要有可能的调试器命令中的限定的名称。 如果想要查看从一个已知的模块的符号，限定使用模块名称;如果您不知道该符号的位置，，使用非限定的名称。 对于本地变量和函数参数，使用**$** 用作模块名称 (例如， *$！MyVar*)。
-   若要诊断的原因的慢速符号加载，激活干扰符号加载 (**SYMOPT\_调试**) 通过使用 **-n**命令行选项或如果调试器已在运行，通过使用 **.symopt + 0x80000000**或 **！ 符号干扰**调试器扩展命令。
-   若要防止调试器搜索中卸载的模块的符号，激活**SYMOPT\_否\_UNQUALIFIED\_加载**通过 **-snul**命令行选项或者，如果调试器已在运行，通过使用 **.symopt + 0x100**。
-   若要显式加载所需的调试会话的模块，使用调试器命令如 **.reload**或**ld**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[WDK 和 WinDbg 下载](https://go.microsoft.com/fwlink/p/?LinkId=733614)

[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063.aspx)

 

 






