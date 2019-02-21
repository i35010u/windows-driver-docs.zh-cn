---
title: 基于堆栈的故障注入
description: 基于堆栈的故障注入选项注入资源故障。 内核模式驱动程序中。
ms.assetid: B5C06413-81FB-46DA-B053-80ED347DA3EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e51b2e851d153436f72a766b4e6bfe866507a24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540658"
---
# <a name="stack-based-failure-injection"></a>基于堆栈的故障注入


**请注意**  的说明启用此功能仅适用于 Windows 8 的 WDK。 对于 Windows 8.1，此功能已集成到驱动程序验证程序。 在运行 Windows 8.1 的计算机，使用[系统资源不足模拟](systematic-low-resource-simulation.md)选项。

 

基于堆栈的故障注入选项注入资源故障。 内核模式驱动程序中。 此选项结合使用了特殊驱动程序 KmAutoFail.sys 和[驱动程序验证程序](driver-verifier.md)来侵入驱动程序错误处理路径。 一直很难测试这些路径。 基于堆栈的故障注入选项以可预测的方式，使它找到可重现问题注入资源故障。 错误路径可轻松地重现，因为它也便于验证这些问题的修补程序。

为了帮助您确定该错误的根本原因，调试器扩展是提供，可以告知用户已插入了完全的失败和以何种顺序。

特定驱动程序上启用了基于堆栈的故障注入选项，它截获对内核和 Ndis.sys 某些调用从该驱动程序。 基于堆栈的故障注入会查看调用堆栈 — 具体来说，在来自驱动程序启用的调用堆栈的一部分。 如果这是它已见过该堆栈的第一次，操作将失败的调用根据该调用的语义。 否则，如果它已注意到之前调用，它会将它传递通过保持不变。 基于堆栈的故障注入包含逻辑来处理这一事实可以加载和卸载多次驱动程序。 它将识别即使驱动程序重新加载到不同的内存位置，调用堆栈是相同。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


后，可以激活一个或多个驱动程序的基于堆栈的故障注入功能[部署到测试计算机的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/deploying_a_driver_to_a_test_computer)。 在配置时，可以选择基于堆栈的故障注入选项[驱动程序包项目的驱动程序验证器属性](https://msdn.microsoft.com/windows-drivers/develop/driver_verifier_properties_for__driver_projects)。 必须重新启动计算机以激活或停用基于堆栈的故障注入选项。 此外可以运行测试实用程序以启用驱动程序验证程序和测试计算机上的此功能。

**重要**  激活时基于堆栈的故障注入测试计算机上，请确保不要还选择[低资源模拟](low-resources-simulation.md)。

 

-   **使用驱动程序验证程序属性页**

    1.  打开你的驱动程序包的属性页。 右键单击驱动程序包项目中的**解决方案资源管理器**，然后选择**属性**。
    2.  在为驱动程序包属性页中，单击**配置属性**，单击**驱动程序安装**，然后单击**Driver Verifier**。
    3.  选择**启用驱动程序验证程序**。 在测试计算机上启用驱动程序验证程序时，您可以选择启用驱动程序验证程序的计算机上，为驱动程序项目的所有驱动程序，或指定的驱动程序的列表。
    4.  下**堆栈基于故障注入器**，选择 （检查） 基于堆栈的故障注入。
    5.  单击 **“应用”** 或 **“确定”**。
    6.  请参阅[部署到测试计算机的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/deploying_a_driver_to_a_test_computer)有关详细信息。 若要激活此选项，必须重新启动测试计算机。
-   **使用启用和禁用驱动程序验证测试**

    1.  此外可以通过运行实用程序测试驱动程序验证程序。 按照中所述的说明[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)。 下**的所有测试\\Driver Verifier**测试类别中，选择**启用驱动程序验证程序 （需要可能重启）** 和**禁用驱动程序验证程序 （可能需要重启必需的）** 测试。
    2.  通过单击名称选择 Driver Verifier 选项**启用驱动程序验证程序 （需要可能重启）** 中的测试**驱动程序测试组**窗口。
    3.  选择 （检查） 堆栈基于故障注入。
    4.  向测试组添加这些测试后可以保存的测试组。 若要启用堆栈基于故障注入，运行**启用驱动程序验证程序 （需要可能重启）** 在已配置用于测试的计算机上进行测试。

        若要停用驱动程序验证程序，请运行**禁用驱动程序验证程序 （需要可能重启）** 测试。

## <a name="span-idusingthestackbasedfailureinjectionoptionspanspan-idusingthestackbasedfailureinjectionoptionspanspan-idusingthestackbasedfailureinjectionoptionspanusing-the-stack-based-failure-injection-option"></a><span id="Using_the_Stack_Based_Failure_Injection_option"></span><span id="using_the_stack_based_failure_injection_option"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION_OPTION"></span>使用基于堆栈的故障注入选项


使用基于堆栈的故障注入测试时的一个重要考虑因素是它找到的 bug 最多将导致的 bug 检查。 这可能会证明某种程度上痛苦，如果您的驱动程序启动加载的驱动程序。 正因为如此，我们会自动将禁用基于堆栈的故障注入如果驱动程序验证程序处于禁用状态。 这意味着，您可以通过禁用驱动程序验证程序使用该命令，在调试器中启动时禁用基于堆栈的故障注入 **！ verifier – 禁用**。

如果可能，为你使用基于堆栈的故障注入的初始测试，设置您的驱动程序，以便在启动时不加载它。 然后可以运行一些简单的负载，并卸载测试。 许多基于堆栈的故障注入所找到的 bug 在初始化或清理期间发生。 重复加载和卸载您的驱动程序是一个好方法找到这些。

后负载所需的任何修补程序卸载测试成功，你可以转到基于 IOCTL 的测试，完整的功能测试和最后压力测试。 一般情况下，如果您遵循此测试进度，您将不发现许多新问题期间压力测试，因为大部分代码路径将已执行在此之前。

## <a name="span-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanspan-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanspan-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanusing-the-stack-based-failure-injection-sbfi-debugger-extension"></a><span id="Using_the_Stack_Based_Failure_Injection__SBFI__debugger_extension"></span><span id="using_the_stack_based_failure_injection__sbfi__debugger_extension"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION__SBFI__DEBUGGER_EXTENSION"></span>使用堆栈基于故障注入 (SBFI) 调试器扩展


检查大部分与基于堆栈的故障注入结果在 bug 中发现的问题。 若要帮助确定这些代码的问题的原因，WDK 提供基于堆栈的故障注入调试器扩展和必需的符号。 安装过程将在调试器系统上同时安装。 默认位置是 c:\\Program Files (x86)\\Windows 工具包\\8.0\\调试器\\*&lt;arch&gt;*。

**若要运行的调试程序扩展**

- 在调试器命令提示符下键入以下命令： **！**<em>&lt;路径&gt;\\</em>**kmautofaildbg.dll.autofail**。 例如，假设调试器扩展安装在 c:\\dbgext 和该 kmautofail.pdb 处于符号路径时，应输入以下命令：

  ```
  !c:\dbgext\kmautofaildbg.dll.autofail
  ```

这将转储到调试器显示从最新的故障注入的调用堆栈信息。 每个条目看起来类似于以下内容，来自实际测试运行。 在以下示例中，基于堆栈的故障注入 Mydriver.sys 上启用

```
Sequence: 2, Test Number: 0, Process ID: 0, Thread ID: 0
                 IRQ Level: 2, HASH: 0xea98a56083aae93c
 0xfffff8800129ed83 kmautofail!ShimHookExAllocatePoolWithTag+0x37
 0xfffff88003c77566 mydriver!AddDestination+0x66
 0xfffff88003c5eeb2 mydriver!ProcessPacketDestination+0x82
 0xfffff88003c7db82 mydriver!ProcessPacketSource+0x8b2
 0xfffff88003c5d0d8 mydriver!ForwardPackets+0xb8
 0xfffff88003c81102 mydriver!RoutePackets+0x142
 0xfffff88003c83826 mydriver!RouteNetBufferLists+0x306
 0xfffff88003c59a76 mydriver!DeviceSendPackets+0x156
 0xfffff88003c59754 mydriver!ProcessingComplete+0x4a4
 0xfffff88001b69b81 systemdriver2!ProcessEvent+0x1a1
 0xfffff88001b3edc4 systemdriver1!CallChildDriver+0x20
 0xfffff88001b3fc0a systemdriver1!ProcessEvent+0x3e
 0xfffff800c3ea6eb9 nt!KiRetireDpcList+0x209
 0xfffff800c3ea869a nt!KiIdleLoop+0x5a
```

在输出的顶部，序列数计数的错误注入的数。 此示例演示了此测试运行期间注入的第二个错误。 进程 ID 为 0，因此这是系统进程。 IRQL 是 2，因此这称为调度级别。

从堆栈，KmAutoFail 是基于堆栈的故障注入驱动程序。 函数名称指示哪个函数将调用从 Mydriver.sys KmAutoFail 被截获和错误注入。 在这里，失败的函数已[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)。 中的所有函数 KmAutoFail 拦截 Ntoskrnl.sys 或 Ndis.sys 对使用此命名约定。 接下来，我们看到调用堆栈与驱动程序正在进行测试 (Mydriver.sys)。 这是用于确定堆栈的唯一性的调用堆栈的一部分。 因此每个条目由调试器扩展转储是在调用堆栈的这一部分唯一的。 调用堆栈的其余部分指示人员称为驱动程序。 主要的重要性是从用户模式 （通过 IOCTL) 或内核模式驱动程序是否调用该驱动程序。

请注意，如果驱动程序已返回故障从其[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，重新加载尝试将通常发生在不同的内存位置。 在这种情况下，从早期的位置的调用堆栈可能将包含"垃圾"，而不是从驱动程序的堆栈信息。 但这不是一个问题：它会告诉您该驱动程序正确地处理该注入的错误。

下面的条目演示如何通过从用户模式 IOCTL 的驱动程序调用。 请注意进程 ID 和 IRQ 级别。 由于 Mydriver.sys NDIS 筛选器驱动程序，IOCTL 是通过 Ndis.sys。 请注意该 nt ！NtDeviceIoControlFile 位于堆栈上。 在您使用 Ioctl 的驱动程序运行任何测试会通过此函数。

```
Sequence: 5, Test Number: 0, Process ID: 2052, Thread ID: 4588
                 IRQ Level: 0, HASH: 0xecd4650e9c25ee4
 0xfffff8800129ed83 kmautofail!ShimHookExAllocatePoolWithTag+0x37
 0xfffff88003c6fb39 mydriver!SendMultipleOids+0x41
 0xfffff88003c7157b mydriver!PvtDisconnect+0x437
 0xfffff88003c71069 mydriver!NicDisconnect+0xd9
 0xfffff88003ca3538 mydriver!NicControl+0x10c
 0xfffff88003c99625 mydriver!DeviceControl+0x4c5
 0xfffff88001559d93 NDIS!ndisDummyIrpHandler+0x73
 0xfffff88001559339 NDIS!ndisDeviceControlIrpHandler+0xc9
 0xfffff800c445cc96 nt!IovCallDriver+0x3e6
 0xfffff800c42735ae nt!IopXxxControlFile+0x7cc
 0xfffff800c4274836 nt!NtDeviceIoControlFile+0x56
 0xfffff800c3e74753 nt!KiSystemServiceCopyEnd+0x13
```

## <a name="span-idanalyzingtheresultsofstackbasedfailureinjectionspanspan-idanalyzingtheresultsofstackbasedfailureinjectionspanspan-idanalyzingtheresultsofstackbasedfailureinjectionspananalyzing-the-results-of-stack-based-failure-injection"></a><span id="Analyzing_the_results_of_Stack_Based_Failure_Injection"></span><span id="analyzing_the_results_of_stack_based_failure_injection"></span><span id="ANALYZING_THE_RESULTS_OF_STACK_BASED_FAILURE_INJECTION"></span>分析基于堆栈的故障注入的结果


在您的驱动程序，运行测试和突然击中问题。 这很可能是错误检查，但也可能由于计算机变得无响应。 如何查找原因？ 假设的 bug 检查，首先使用上述扩展若要查找的注入失败列表并使用调试器命令： **！ 分析 – v**。

最常见的 bug 检查引起不检查的分配成功。 在这种情况下，从 bug 检查分析堆栈是到的最后一个故障注入可能几乎完全相同。 在某些时候失败分配 （通常非常下一行） 后，该驱动程序将访问 null 指针。 这种类型是 bug 的很容易修复。 失败分配有时是一个或两个列表，但此类型仍是很容易查找和修复。

在清理期间出现的另一种最常见的 bug 检查。 在这种情况下，该驱动程序可能检测到分配失败和跳转到清除;但在清理时，该驱动程序未选中该指针并再一次访问 null 指针。 密切相关的用例是其中两次调用清理。 如果清理不未设置为一种结构来为 null 后将其释放的指针，第二次调用清理函数它将尝试释放结构第二次，从而导致的 bug 检查。

导致计算机变得无响应的错误会更加困难，若要诊断，但若要对其进行调试的过程类似。 这些错误通常由引用计数，或启动锁定问题。 幸运的是， [Driver Verifier](driver-verifier.md)之前它们会导致问题，将捕获许多数值调节钮锁定问题。 在这些情况下，在调试器中中断，并使用调试器扩展转储的已通过基于堆栈的故障注入插入错误的列表。 快速了解最新故障周围的代码可能会显示的引用计数是在发生故障之前执行，但之后不发布。 如果没有，请您旋转锁，正在等待的驱动程序中的线程或显然是错误的任何引用计数。

 

 





