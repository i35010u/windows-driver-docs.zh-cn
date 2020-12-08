---
title: 驱动程序的代码分析概述
description: Windows 驱动程序工具包为 Microsoft Visual Studio Ultimate 2012 中的代码分析工具提供了特定于驱动程序的扩展。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f598f3f1311e3b1936f516a48a7ec4cb36f7758a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795113"
---
# <a name="code-analysis-for-drivers-overview"></a>驱动程序的代码分析概述


Windows 驱动程序工具包为 Microsoft Visual Studio 中的 [代码分析工具](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120)) 提供了特定于驱动程序的扩展。 驱动程序的代码分析包括仅适用于驱动程序（特别是内核模式驱动程序）的规则。 如果代码可以编译，则驱动程序的代码分析会立即检测到代码中的潜在错误。

## <a name="span-idhow_the_code_analysis_tool_worksspanspan-idhow_the_code_analysis_tool_worksspanspan-idhow_the_code_analysis_tool_worksspanhow-the-code-analysis-tool-works"></a><span id="How_the_Code_Analysis_tool_works"></span><span id="how_the_code_analysis_tool_works"></span><span id="HOW_THE_CODE_ANALYSIS_TOOL_WORKS"></span>代码分析工具的工作原理


代码分析工具会截获生成实用工具对标准编译器的调用，Cl.exe，而是运行 CL 截取编译器来分析驱动程序源代码，并创建错误和警告消息的日志文件。 您可以单独运行代码分析工具，也可以配置在生成驱动程序时运行的代码分析工具。 当你运行代码分析工具本身 (**分析 &gt; 对解决方案运行代码分析** 时) 结果将显示在 "代码分析报表" 窗口中。 当您在生成过程中运行代码分析工具时，CL 截取编译器将创建错误和警告消息的日志文件，然后调用 Cl.exe 的标准版本来生成生成输出。 生成的对象文件与标准生成命令所生成的文件相同。

当截获编译器运行时，针对驱动程序的代码分析将单独检查代码中的每个函数，然后通过代码模拟所有可能路径的执行，寻找常见的驱动程序错误和不明智的编码做法。 即使在较大的驱动程序上，代码分析工具也会相对快捷地运行，并且它生成的报表会精确地标识驱动程序代码的行，并出现可疑错误。

## <a name="span-idthe_types_of_errors_code_analysis_can_detectspanspan-idthe_types_of_errors_code_analysis_can_detectspanspan-idthe_types_of_errors_code_analysis_can_detectspanthe-types-of-errors-code-analysis-can-detect"></a><span id="The_types_of_errors_Code_Analysis_can_detect"></span><span id="the_types_of_errors_code_analysis_can_detect"></span><span id="THE_TYPES_OF_ERRORS_CODE_ANALYSIS_CAN_DETECT"></span>代码分析的错误类型可以检测


代码分析可以检测到多种类型的错误，包括以下类别中的错误：

-   **内存：** 潜在的内存泄漏，取消引用的 **空** 指针，访问未初始化的内存，过度使用内核模式堆栈，并且不恰当地使用池标记。

-   **资源：** 无法释放资源（如锁、调用某些函数时应持有的资源）以及调用其他函数时不应持有的资源。

-   **函数使用：** 可能不正确地使用某些函数、出现不正确的函数参数、不严格检查类型的函数的可能的参数类型不匹配、是否可能使用某些已过时的函数，以及在可能不正确的 IRQL 上函数调用。

-   **浮点状态：** 未能保护驱动程序中的浮点硬件状态，并在将其保存到不同的 IRQL 后尝试还原浮点状态。

-   **优先规则：** 由于 C 编程的优先规则，可能不会表现为程序员所需的代码。

-   **内核模式编码做法：** 编码做法会导致错误，例如修改不透明的内存描述符列表 (MDL) 结构，无法检查被调用函数设置的变量的值，而是使用 C/c + + 字符串操作函数，而不是在 Ntstrsafe.h 而中定义的安全字符串函数。

-   **特定于驱动程序的编码做法：** 通常是内核模式驱动程序中的错误源的特定操作。 例如，在不修改成员的情况下，将整个 i/o 请求数据包复制 (IRP) ，而不是在 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程中复制参数。

## <a name="span-idcode_analysis_warningsspanspan-idcode_analysis_warningsspanspan-idcode_analysis_warningsspancode-analysis-warnings"></a><span id="Code_Analysis_warnings"></span><span id="code_analysis_warnings"></span><span id="CODE_ANALYSIS_WARNINGS"></span>代码分析警告


代码分析工具使用基于规则的模型来识别程序或驱动程序代码中的错误。 每个规则都与一个警告相关联，如果代码分析工具检测到规则冲突，则会报告该警告。 有关特定于驱动程序的警告的详细信息，请参阅 [针对驱动程序警告的代码分析](prefast-for-drivers-warnings.md)。 有关 Visual Studio 中的代码分析工具报告的核心警告集的信息，请参阅 [代码分析警告](/previous-versions/visualstudio/visual-studio-2012/a5b9aa09(v=vs.110))。

## <a name="span-idannotationsspanspan-idannotationsspanspan-idannotationsspanannotations"></a><span id="Annotations"></span><span id="annotations"></span><span id="ANNOTATIONS"></span>批注


代码分析工具提供的一项重要功能是能够批注驱动程序源代码中的函数说明和其他一些实体。 代码分析工具具有功能范围内的范围;也就是说，它会分析函数之间的交互。 批注的目标是为调用函数和调用函数之间的协定提供更完整的表达式，以便代码分析工具可以检查是否满足约定。 批注的另一个目标是，它们会通知任何代码读取了应如何使用函数的代码和预期的结果。 批注声明接口的协定，并且不尝试说明该协定是如何实现的。 在许多情况下，运行代码分析工具的结果会反映缺少相应的批注，并且通过添加批注，会禁止显示缺失批注的警告，并启用其他检查。 有关详细信息，请参阅 [Windows 驱动程序的 SAL 2.0 批注](sal-2-annotations-for-windows-drivers.md)。 有关 SAL 2.0 的详细信息，请参阅 [使用 Sal 注释减少 C/c + + 代码缺陷](/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)。 SAL 2.0 替换 SAL 1.0。 SAL 2.0 应与适用于 Windows 8 的 WDK 一起使用。 如果需要有关 SAL 1.0 的驱动程序的信息，请参阅随 WDK for Windows 7 附带的 PREfast for 驱动程序批注文档。

## <a name="span-idinterpreting_the_resultspanspan-idinterpreting_the_resultspanspan-idinterpreting_the_resultspaninterpreting-the-result"></a><span id="Interpreting_the_result"></span><span id="interpreting_the_result"></span><span id="INTERPRETING_THE_RESULT"></span>解释结果


驱动程序的代码分析易于运行，并且即使在非常大的驱动程序和程序上，也能快速运行。 开发人员的工作是检查输出，分析代码分析工具检测到的错误，并将代码分析工具误解的有效代码中的实际编码错误区分开来。

有关描述代码分析工具可能检测到的每个警告的全面参考，请参阅 [针对驱动程序警告的代码分析](prefast-for-drivers-warnings.md)。 有关 Visual Studio 中的代码分析工具报告的核心警告集的信息，请参阅 [代码分析警告](/cpp/code-quality/code-analysis-for-c-cpp-warnings)。

解决代码分析警告通常涉及在适当情况下更新源代码，或添加批注来阐明函数协定。 添加批注后，分析器就可以对所有将来的调用方强制协定，还可以提高可读性。

如果 **代码分析结果** 显示你确定的错误（在仔细检查后）无效，并且即使使用批注，也不能避免使用，则可以选择排除或禁止显示这些警告。 有关详细信息，请参阅 [如何对驱动程序运行代码分析](how-to-run-code-analysis-for-drivers.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[如何为驱动程序运行“代码分析”](how-to-run-code-analysis-for-drivers.md)

[Visual Studio 中的代码分析工具](/visualstudio/code-quality/)

[驱动程序的代码分析警告](prefast-for-drivers-warnings.md)

[代码分析警告](/cpp/code-quality/code-analysis-for-c-cpp-warnings)

[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)

 

