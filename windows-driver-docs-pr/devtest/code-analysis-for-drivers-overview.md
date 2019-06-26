---
title: 驱动程序的代码分析概述
description: Windows 驱动程序工具包提供了 Microsoft Visual Studio Ultimate 2012 中的代码分析工具的特定于驱动程序的扩展。
ms.assetid: 2A780608-F386-4838-A4EB-022C2F0EED3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b775f9e6a8d7ae59dfe91045577b4016bee7ae8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371620"
---
# <a name="code-analysis-for-drivers-overview"></a>驱动程序的代码分析概述


Windows 驱动程序工具包提供的特定于驱动程序的扩展[代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)Microsoft Visual Studio 中。 Code Analysis for Drivers 包括仅适用于驱动程序，尤其是内核模式驱动程序的规则。 驱动程序的代码分析可以在代码中检测潜在的错误，就立即可以编译代码。

## <a name="span-idhowthecodeanalysistoolworksspanspan-idhowthecodeanalysistoolworksspanspan-idhowthecodeanalysistoolworksspanhow-the-code-analysis-tool-works"></a><span id="How_the_Code_Analysis_tool_works"></span><span id="how_the_code_analysis_tool_works"></span><span id="HOW_THE_CODE_ANALYSIS_TOOL_WORKS"></span>代码分析工具的工作原理


代码分析工具截获对标准编译器 Cl.exe 生成实用程序的调用，并改为，运行分析驱动程序源代码，并创建一个日志文件的错误和警告消息的 CL 截距编译器。 可以运行代码分析工具本身，也可以配置代码分析工具运行时构建您的驱动程序。 当通过自身运行代码分析工具时 (**分析&gt;对解决方案运行代码分析**) 在代码分析报告窗口中显示结果。 当作为生成的一部分运行代码分析工具时，CL 截距编译器创建的错误和警告消息的日志文件，然后它调用 Cl.exe 以产生生成输出的标准版本。 作为这些由标准生成命令，生成的对象文件都是相同的。

截取编译器在运行时，Code Analysis for Drivers 独立检查代码中的每个函数，然后模拟执行所有可能的路径执行代码，查找常见驱动程序错误和不明智的编码做法。 代码分析工具运行相对较快，甚至对较大的驱动程序，并准确地说它生成报表标识怀疑有错误的驱动程序代码行。

## <a name="span-idthetypesoferrorscodeanalysiscandetectspanspan-idthetypesoferrorscodeanalysiscandetectspanspan-idthetypesoferrorscodeanalysiscandetectspanthe-types-of-errors-code-analysis-can-detect"></a><span id="The_types_of_errors_Code_Analysis_can_detect"></span><span id="the_types_of_errors_code_analysis_can_detect"></span><span id="THE_TYPES_OF_ERRORS_CODE_ANALYSIS_CAN_DETECT"></span>代码分析可检测的错误类型


代码分析可以检测到多种类型的错误，包括以下类别中的错误：

-   **内存：** 潜在的内存泄漏，取消引用**NULL**指针，访问未初始化的内存、 内核模式堆栈的过度使用和不正确使用池标记。

-   **资源：** 发布资源，如锁、 调用某些函数时应保留的资源和资源的调用其他函数时不应保存失败。

-   **函数，请使用：** 某些功能可能不正确使用，会显示不正确，则可能参数的函数参数类型不匹配的函数的不严格检查类型，可能使用某些已过时的函数，并在调用函数可能IRQL 不正确。

-   **浮点状态：** 保护浮点硬件状态中的驱动程序并将其保存在不同的 IRQL 后还原的浮点状态的尝试失败。

-   **优先顺序规则：** 可能不会作为程序员不由于 C 编程的优先规则的代码。

-   **内核模式的编码实践：** 编码实践，可能会导致错误，例如修改不透明内存描述符列表 (MDL) 结构，对故障调用函数，通过检查设置变量的值以及使用 C /C++而不是安全字符串的字符串操作函数Ntstrsafe.h 中定义的函数。

-   **特定于驱动程序的编码做法：** 通常是内核模式驱动程序中的错误的源的特定操作。 例如，复制整个的 I/O 请求数据包 (IRP) 而无需修改成员并将一个指针保存到一个字符串或结构的参数，而不是复制中的自变量[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。

## <a name="span-idcodeanalysiswarningsspanspan-idcodeanalysiswarningsspanspan-idcodeanalysiswarningsspancode-analysis-warnings"></a><span id="Code_Analysis_warnings"></span><span id="code_analysis_warnings"></span><span id="CODE_ANALYSIS_WARNINGS"></span>代码分析警告


代码分析工具使用基于规则的模型来确定程序或驱动程序代码中的错误。 每个规则都与代码分析工具检测到违反规则时报告警告相关联。 有关特定于驱动程序的警告的详细信息，请参阅[的代码分析驱动程序警告](prefast-for-drivers-warnings.md)。 Visual Studio 中的代码分析工具报告的警告的核心集有关的信息，请参阅[代码分析警告](https://go.microsoft.com/fwlink/p/?linkid=226853)。

## <a name="span-idannotationsspanspan-idannotationsspanspan-idannotationsspanannotations"></a><span id="Annotations"></span><span id="annotations"></span><span id="ANNOTATIONS"></span>批注


代码分析工具提供的重要功能之一是能够批注函数说明和驱动程序的源代码中的某些其他实体。 代码分析工具具有内部功能的作用域;也就是说，它将分析函数之间的交互。 批注的目的是协定的提供名为和调用函数之间的更完整的表达式，以便代码分析工具可检查符合协定。 批注的另一个目标是他们告知任何人读取应如何使用该函数的代码，并可以预期的结果。 批注声明接口的协定，并不试图介绍如何实现该协定。 在许多情况下，运行代码分析工具的结果反映没有相应批注，并且通过添加批注，抑制缺少批注有关的警告，和启用了其他检查。 有关详细信息，请参阅[SAL 2.0 注释为 Windows 驱动程序](sal-2-annotations-for-windows-drivers.md)。 有关 SAL 2.0 的详细信息，请参阅[使用 SAL 注释减少 C /C++代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)。 SAL 2.0 替换 SAL 1.0。 SAL 2.0 应在 Windows 8 的 WDK。 如果驱动程序需要有关 SAL 1.0 的信息，请参阅 WDK 为 Windows 7 附带的驱动程序批注文档 PREfast。

## <a name="span-idinterpretingtheresultspanspan-idinterpretingtheresultspanspan-idinterpretingtheresultspaninterpreting-the-result"></a><span id="Interpreting_the_result"></span><span id="interpreting_the_result"></span><span id="INTERPRETING_THE_RESULT"></span>解释结果


驱动程序的代码分析是可以方便地运行，运行速度很快，甚至在很大的驱动程序和程序。 检查输出，分析的错误的代码分析工具检测到，并使实际编码错误的代码分析工具会错误地解释的有效代码开发人员的工作。

介绍代码分析工具可能检测到每个警告的全面参考，请参阅[的代码分析驱动程序警告](prefast-for-drivers-warnings.md)。 Visual Studio 中的代码分析工具报告的警告的核心集有关的信息，请参阅[代码分析警告](https://go.microsoft.com/fwlink/p/?linkid=226853)。

解决代码分析警告通常涉及到更新的源代码，如果合适，或添加批注以阐明函数协定。 添加批注，该分析器，以强制执行所有未来调用方的约定，它还提高了可读性。

如果**代码分析结果**确定，请仔细检查后显示错误无效，无法避免甚至与使用批注，则可以选择排除或取消这些警告。 有关详细信息，请参阅[如何运行代码分析的驱动程序](how-to-run-code-analysis-for-drivers.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何为驱动程序运行“代码分析”](how-to-run-code-analysis-for-drivers.md)

[在 Visual Studio 中的代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)

[代码分析驱动程序警告](prefast-for-drivers-warnings.md)

[代码分析警告](https://go.microsoft.com/fwlink/p/?linkid=226853)

[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)

 

 






