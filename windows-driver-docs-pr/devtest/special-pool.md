---
title: 驱动程序验证器中的特殊池内存损坏检测
description: 若要检测内存损坏情况，驱动程序验证程序可以从特殊池分配驱动程序内存，并监视该池是否有不正确的访问权限。
ms.assetid: b1381a75-279a-42b7-b18d-43aba796424b
keywords:
- 特殊池功能 WDK 驱动程序验证程序
- 内存损坏 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2dfbcb93fc0471d17963896c5d8da8c12fc4824
ms.sourcegitcommit: 441900007a5c1c784fb7f426e0a2a570923e21a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2020
ms.locfileid: "92499512"
---
# <a name="special-pool-memory-corruption-detection-in-driver-verifier"></a>驱动程序验证器中的特殊池内存损坏检测

内存损坏是常见的驱动程序问题。 出现错误后，驱动程序错误可能导致过长。 最常见的错误是访问已释放的内存，并分配 *n* 个字节，然后访问 *n*+ 1 个字节。

若要检测内存损坏情况，驱动程序验证程序可以从特殊池分配驱动程序内存，并监视该池是否有不正确的访问权限。 为内核模式系统提供的例程（如 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ）以及 GDI 系统提供的例程（如 [**EngAllocMem**](/windows/win32/api/winddi/nf-winddi-engallocmem)）提供特殊池支持。

## <a name="special-pool-by-alignments"></a>按对齐的特殊池

特殊池的两种对齐方式可用：

* **验证开始**对齐更好于检测访问不足。
* **验证结束**对齐更好于检测访问超限。

有关如何使用 **验证开始** 和 **验证结束** 选项的详细信息，请参阅 [检测超支和不足](../debugger/detecting-overruns-and-underruns.md)。 请注意，绝大多数内存损坏都是由于 *溢出*，而不是不足。

当 "特殊池" 功能处于活动状态且已选择 " **结束** " 时，驱动程序请求的每个内存分配都将放置在单独的页面上。 返回允许分配在页面上容纳的最大可能地址，以便内存与页面末尾对齐。 页面的上一部分以特殊模式写入。 上一页和下一页被标记为不可访问。

如果驱动程序在分配结束后尝试访问内存，驱动程序验证程序将立即检测到这一点，并将发出 [**Bug 检查 0xCD**](../debugger/bug-check-0xcd--page-fault-beyond-end-of-allocation.md)。 如果驱动程序在缓冲区开头之前的内存中写入，这会 (可能) 更改模式。 当释放缓冲区时，驱动程序验证程序将检测到更改，并发出 [**Bug 检查 0xC1**](../debugger/bug-check-0xc1--special-pool-detected-memory-corruption.md)。

如果驱动程序在释放后读取或写入缓冲区，驱动程序验证程序将发出 [**Bug 检查 0xCC**](../debugger/bug-check-0xcc--page-fault-in-freed-special-pool.md)。

选中 " **验证开始** " 时，内存缓冲区与页面的开头对齐。 使用此设置时，不足将导致立即进行错误检查，并在释放内存时导致 bug 检查。 此选项与 " **验证结束** " 选项相同。

**验证 End** 是否为默认对齐方式，因为超限错误比不足错误更常见。

单个内存分配可以覆盖这些设置，并通过在*优先级*参数设置为 XxxSpecialPoolOverrun 或 XxxSpecialPoolUnderrun 的情况调用[**ExAllocatePoolWithTagPriority**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)来选择其对齐方式。  (此例程无法激活或停用特殊池功能，或请求内存分配的特殊池，否则将从正常池进行分配。 只能从此例程控制对齐方式。 ) 

在 windows 7 和更高版本的 Windows 操作系统中，"特殊池" 选项支持使用以下内核 Api 分配的内存：

* [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

* [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 以及可以 (IRP) 数据结构分配 i/o 请求包的其他例程

* [**RtlAnsiStringToUnicodeString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring) 和其他运行时库 (RTL) 字符串例程

* [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

## <a name="special-pool-by-pool-tag-or-allocation-size"></a>按池标记或分配大小的特殊池

除了使用驱动程序验证程序的特殊池功能（该功能请求由指定的 *驱动程序*分配的特殊池）之外，还有两种方法可以使用特殊池：

* **池标记。** 使用指定的池标记请求所有分配的特殊池。

* **大小。** 请求指定大小范围内的所有分配的特殊池。

若要为池标记或大小范围请求特殊的池，请使用 Gflags，它是 *Windows 调试工具*中包含的工具。 有关详细信息，请参阅 [使用全局标志实用程序](using-the-global-flags-utility.md)。

可以同时使用驱动程序验证程序的特殊池功能和 Gflags 的特殊池功能。 如果执行此操作，请记住，特殊池会受到限制，这并不是所有尝试从特殊池进行分配的操作都将成功，并且 Windows 将返回成功的失败尝试状态，尝试从常规内存池中的分配满足的特定池进行分配。

### <a name="special-pool-efficiency"></a>特殊池效率

并非所有特殊的池请求均已完成。 每个来自特殊池的分配都使用一页不可分页物理内存和两页虚拟地址空间。 如果池用尽，则会以标准方式分配内存，直到特殊池再次变为可用。 当从标准池中填充特殊的池请求时，请求函数不会返回错误，因为池请求已成功。 因此，如果激活了特殊池功能，不建议同时验证多个驱动程序。

使多个小内存请求的单个驱动程序也可以耗尽此池。 如果发生这种情况，最好将池标记分配给驱动程序的内存分配，并将特殊池一次专用于一个池标记。

特殊池的大小增加了系统上的物理内存量;理想情况下，应至少为1千兆字节 (GB) 。 在 x86 计算机上，由于除使用物理) 空间之外的虚拟 (，因此请不要使用 [**/3gb**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200) boot 选项。 最好是将页面文件的最小/最大数量提高一倍。

若要确保正在测试驱动程序的所有分配，建议使用长时间压力过大驱动程序。

## <a name="monitoring-the-special-pool"></a>监视特殊池

可以监视与池分配相关的统计信息。 驱动程序验证程序管理器、Verifier.exe 命令行或日志文件可显示这些项。 有关详细信息，请参阅 [监视全局计数器](monitoring-global-counters.md) 。

如果 " **在特殊池分配成功** " 计数器与 " **池分配成功** " 计数器相等，则特殊池足以涵盖所有内存分配。 如果前一个计数器小于后一个计数器，则已至少用完一次特殊池。

这些计数器不跟踪大小为一页或更大的分配，因为特殊池不适用于它们。

如果启用了 "特殊池" 功能，但未从特殊池分配所有池分配的95%，则驱动程序验证器管理器中会出现警告。 在 Windows 2000 中，此警告将显示在 " **驱动程序状态** " 屏幕上。 在 Windows XP 和更高版本中，此警告会出现在 **全局计数器** 屏幕上。 如果出现这种情况，你应该验证更短的驱动程序列表，按池标记验证单个池，或者向系统添加更多物理内存。

内核调试器扩展 **！ verifier** 还可用于监视特殊池使用情况。 它为驱动程序验证器管理器提供了类似的信息。 有关调试器扩展的信息，请参阅 [Windows 调试](../debugger/index.md)。

### <a name="activating-the-special-pool-option"></a>激活 "特殊池" 选项

你可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活特殊池功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

> [!NOTE]
> 若要按池标记或分配大小激活特殊池功能，或者要设置 **验证开始** (检测不足) 并 **验证最终** (检测溢出) 对齐方式，请使用 [全局标志实用程序](using-the-global-flags-utility.md);这些对齐设置适用于所有特殊池分配。

* **在命令行中**

    在命令行中，特殊池选项由 **位 0 (0x1) **表示。 若要激活特殊池，请使用 "0x1" 标志值或 "将0x1 添加到标志" 值。 例如：

    ``` console
    verifier /flags 0x1 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows 2000 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，来激活和停用特殊池，而无需重新启动计算机。 例如：

    ``` console
    verifier /volatile /flags 0x1 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    标准设置中还包括了特殊的池功能。 例如：

    ``` console
    verifier /standard /driver MyDriver.sys
    ```

* **使用驱动程序验证器管理器**

   1. 选择 " **为代码开发人员 (创建自定义设置") ** ，然后单击 " **下一步**"。
   2. 选择 " **从完整列表中选择单个设置**"。
   3. 选择 (检查) **特殊池**。

    标准设置中还包括了特殊的池功能。 若要使用此功能，请在驱动程序验证器管理器中单击 " **创建标准设置**"。
