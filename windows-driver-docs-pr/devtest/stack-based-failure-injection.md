---
title: 基于堆栈的错误注入
description: 基于堆栈的故障注入选项注入内核模式驱动程序中的资源故障。
ms.assetid: B5C06413-81FB-46DA-B053-80ED347DA3EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3314c8904bb98c57ed1dc58486e9a9bf4cc3e211
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383465"
---
# <a name="stack-based-failure-injection"></a>基于堆栈的错误注入


**注意**   启用此功能的说明仅适用于适用于 Windows 8 的 WDK。 对于 Windows 8.1，此功能已集成到驱动程序验证程序中。 在运行 Windows 8.1 的计算机上，使用 " [系统低资源" 模拟](systematic-low-resource-simulation.md) 选项。

 

基于堆栈的故障注入选项注入内核模式驱动程序中的资源故障。 此选项结合使用了特殊驱动程序 KmAutoFail.sys 和[驱动程序验证程序](driver-verifier.md)来侵入驱动程序错误处理路径。 过去，测试这些路径是非常困难的。 基于堆栈的故障注入选项以可预测的方式注入资源故障，这会使其发现的问题可重现。 由于错误路径容易重现，因此还可以轻松验证这些问题的修复。

为了帮助您确定错误的根本原因，提供了一个调试器扩展，它可以准确地告诉您哪些失败已注入并按何种顺序排列。

如果在特定的驱动程序上启用了基于堆栈的故障注入选项，则会将该驱动程序的某些调用截获到内核，并 Ndis.sys。 基于堆栈的故障注入查看调用堆栈，具体而言，就是在其上启用了该驱动程序的调用堆栈的一部分。 如果这是第一次看到该堆栈，则会根据调用的语义使调用失败。 否则，如果在之前已发现调用，它将通过保持不变。 基于堆栈的故障注入包含用于处理某个驱动程序可以加载并多次卸载这一事实的逻辑。 即使将驱动程序重装到不同的内存位置，它也会识别出调用堆栈是否相同。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


在将 [驱动程序部署到测试计算机](/windows-hardware/drivers)时，可以激活一个或多个驱动程序的基于堆栈的故障注入功能。 [为驱动程序包项目配置驱动程序验证程序属性](/windows-hardware/drivers)时，可以选择 "基于堆栈的故障注入" 选项。 您必须重新启动计算机，以激活或停用基于堆栈的故障注入选项。 你还可以运行测试实用工具，在测试计算机上启用驱动程序验证程序和此功能。

**重要提示**   当你在测试计算机上激活基于堆栈的故障注入时，请确保不要同时选择[低资源模拟](low-resources-simulation.md)。

 

-   **使用 "驱动程序验证程序" 属性页**

    1.  打开驱动程序包的属性页。 在 **解决方案资源管理器** 中右键单击驱动程序包项目，然后选择 " **属性**"。
    2.  在驱动程序包的属性页中，单击 " **配置属性**"，单击 " **驱动程序安装**"，然后单击 " **驱动程序验证程序**"。
    3.  选择 " **启用驱动程序验证程序**"。 在测试计算机上启用驱动程序验证程序时，可以选择为计算机上的所有驱动程序、仅针对驱动程序项目或指定驱动程序的列表启用驱动程序验证程序。
    4.  在 " **基于堆栈的故障注入器**" 下，选择 " (检查) 基于堆栈的故障注入"。
    5.  单击 **“应用”** 或 **“确定”**。
    6.  有关详细信息，请参阅 [将驱动程序部署到测试计算机](/windows-hardware/drivers) 。 必须重新启动测试计算机才能激活此选项。
-   **使用启用和禁用驱动程序验证程序测试**

    1.  还可以通过运行实用工具测试来启用驱动程序验证程序。 按照 [如何使用 Visual Studio 在运行时测试驱动程序](/windows-hardware/drivers)中所述的说明进行操作。 在 " **所有测试 \\ 驱动程序验证程序** " 测试类别下，选择 " **启用驱动程序验证程序 (可能需要重新启动") ** 并 **禁用驱动程序验证程序 (可能需要重新启动) ** 测试。
    2.  通过在 "**驱动程序测试组**" 窗口中单击 "**启用驱动程序验证程序 (可能需要重新启动) ** ，选择" 驱动程序验证程序 "选项。
    3.  选择 (检查) 基于堆栈的失败注入。
    4.  将这些测试添加到测试组后，可以保存测试组。 若要启用基于堆栈的故障注入，请在已配置用于测试的计算机上运行 " **启用驱动程序验证程序 (可能需要重新启动) ** 测试"。

        若要停用驱动程序验证程序，请运行 " **禁用驱动程序验证程序" (需要重新启动) ** 测试。

## <a name="span-idusing_the_stack_based_failure_injection_optionspanspan-idusing_the_stack_based_failure_injection_optionspanspan-idusing_the_stack_based_failure_injection_optionspanusing-the-stack-based-failure-injection-option"></a><span id="Using_the_Stack_Based_Failure_Injection_option"></span><span id="using_the_stack_based_failure_injection_option"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION_OPTION"></span>使用基于堆栈的故障注入选项


使用基于堆栈的故障注入进行测试时，需要注意的一个重要事项是，它找到的大多数 bug 都将导致 bug 检查。 如果你的驱动程序是启动加载的驱动程序，这可能会很麻烦。 因此，如果禁用了驱动程序验证程序，则会自动禁用基于堆栈的故障注入。 这意味着，你可以通过使用命令 **！ verifier-disable**禁用驱动程序验证程序，在启动时从调试器禁用基于堆栈的故障注入。

如果可能，请将你的驱动程序设置为在启动时不加载该驱动程序，以便在初始测试中注入基于堆栈的故障。 然后，可以运行一些简单的加载和卸载测试。 基于堆栈的故障注入发现的许多 bug 都在初始化或清理过程中发生。 重复加载和卸载驱动程序是查找这些问题的好方法。

进行必要的修复以使加载卸载测试成功完成后，您可以转到基于 IOCTL 的测试、功能完整的测试，最后进行压力测试。 通常，如果按照此测试进度进行，则在负载测试过程中将不会发现许多新问题，因为在此之前，大多数代码路径都已执行。

## <a name="span-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanspan-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanspan-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanusing-the-stack-based-failure-injection-sbfi-debugger-extension"></a><span id="Using_the_Stack_Based_Failure_Injection__SBFI__debugger_extension"></span><span id="using_the_stack_based_failure_injection__sbfi__debugger_extension"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION__SBFI__DEBUGGER_EXTENSION"></span>使用基于堆栈的故障注入 (SBFI) 调试程序扩展


基于堆栈故障注入发现的大多数问题都将导致 bug 检查。 为了帮助确定这些代码 bug 的原因，WDK 提供了基于堆栈的故障注入调试器扩展和必要的符号。 安装过程将同时在您的调试器系统上安装。 默认位置为 C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.0 \\ 调试 \\ * &lt; &gt; *程序 "。

**运行调试器扩展**

- 在调试器命令提示符下，键入以下命令： **！**<em> &lt; 路径 &gt;kmautofaildbg.dll \\ </em> ** autofail**。 例如，假定在 c： dbgext 安装了调试器扩展， \\ 并且 kmautofail 在符号路径中，则应输入以下命令：

  ```
  !c:\dbgext\kmautofaildbg.dll.autofail
  ```

这会将信息转储到调试器，并显示来自注入的最新失败的调用堆栈。 每个条目都如下所示，从真实的测试运行开始。 在下面的示例中，基于堆栈的故障注入在 Mydriver.sys 上启用

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

在输出的顶部，序列号会对插入的错误数进行计数。 此示例显示了在此测试运行过程中注入的第二个错误。 进程 ID 为0，因此这是系统进程。 IRQL 是2，因此在调度级别调用。

从堆栈中，KmAutoFail 是基于堆栈的故障注入驱动程序。 KmAutoFail 函数名称指示 Mydriver.sys 中被截获并注入错误的函数调用。 此处，失败的函数已 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)。 KmAutoFail 中用于截获对 Ntoskrnl.sys 或 Ndis.sys 的调用的所有函数都使用此命名约定。 接下来，我们将看到带有正在测试的驱动程序的调用堆栈 ( # A0) 。 这是调用堆栈中用于确定堆栈的唯一性的部分。 因此，调试器扩展转储的每个项在调用堆栈的此部分中都是唯一的。 调用堆栈的其余部分指示调用了驱动程序的人员。 此方法的主要重要性是从用户模式 (通过 IOCTL) 还是从内核模式驱动程序调用驱动程序。

请注意，如果驱动程序从其 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程返回了故障，则通常会在不同的内存位置发生重载尝试。 在这种情况下，来自前面位置的调用堆栈可能包含 "垃圾"，而不是来自驱动程序的堆栈信息。 但这并不是问题;它告诉您驱动程序已正确地处理了注入的错误。

下一项显示通过用户模式的 IOCTL 对驱动程序的调用。 记下进程 ID 和 IRQ 级别。 由于 Mydriver.sys 是 NDIS 筛选器驱动程序，因此 IOCTL 通过 Ndis.sys。 请注意，nt！NtDeviceIoControlFile 在堆栈上。 在使用 IOCTLs 的驱动程序上运行的任何测试都将通过此函数。

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

## <a name="span-idanalyzing_the_results_of_stack_based_failure_injectionspanspan-idanalyzing_the_results_of_stack_based_failure_injectionspanspan-idanalyzing_the_results_of_stack_based_failure_injectionspananalyzing-the-results-of-stack-based-failure-injection"></a><span id="Analyzing_the_results_of_Stack_Based_Failure_Injection"></span><span id="analyzing_the_results_of_stack_based_failure_injection"></span><span id="ANALYZING_THE_RESULTS_OF_STACK_BASED_FAILURE_INJECTION"></span>分析基于堆栈的故障注入的结果


你正在驱动程序上运行测试，并且突然遇到问题。 这很可能是错误检查，但也可能是因为计算机没有响应。 如何查找原因？ 假设它是 bug 检查，请首先使用上面的扩展查找注入的失败列表，然后使用调试器命令： **！分析– v**。

最常见的 bug 检查是由不检查分配是否成功导致的。 在这种情况下，bug 检查分析中的堆栈可能与注入最后一个失败的堆栈几乎完全相同。 在失败分配之后的某个时刻 (经常) 的下一行，驱动程序将访问 null 指针。 这种类型的错误很容易修复。 有时失败的分配是列表中的一个或两个，但此类型仍非常易于查找并修复。

第二次最常见的 bug 检查在清理过程中发生。 在这种情况下，驱动程序可能检测到分配失败，跳过清理;但在清理过程中，驱动程序不会检查指针，并再次访问 null 指针。 紧密相关的情况是可以调用两次清理。 如果清除不将指向结构的指针设置为在释放该函数后将其设置为 null，则第二次调用清理函数时，它将尝试再次释放该结构，导致 bug 检查。

导致计算机停止响应的错误更难诊断，但用于调试它们的过程与此类似。 这些错误通常是由引用计数或旋转锁问题导致的。 幸运的是， [驱动程序验证](driver-verifier.md) 器会在导致问题之前捕获许多自旋锁问题。 在这些情况下，请中断调试器，并使用调试器扩展来转储由基于堆栈的故障注入注入的错误列表。 有关最新失败的代码的快速查看可能会显示一个引用计数，该计数是在发生故障之前，但在之后未释放。 如果没有，请在驱动程序中查找正在等待旋转锁定的线程，或查找明显错误的任何引用计数。

 

