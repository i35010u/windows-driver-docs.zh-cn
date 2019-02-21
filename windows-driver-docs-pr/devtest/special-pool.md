---
title: 特殊的池
description: 特殊的池
ms.assetid: b1381a75-279a-42b7-b18d-43aba796424b
keywords:
- 特殊池功能 WDK Driver Verifier
- WDK 驱动程序验证程序的内存损坏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e20ecd0216b2556780281d2af4c424c346628a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533675"
---
# <a name="special-pool"></a>特殊的池


## <span id="ddk_special_memory_pool_tools"></span><span id="DDK_SPECIAL_MEMORY_POOL_TOOLS"></span>


内存损坏是常见的驱动程序问题。 长时间进行错误之后，驱动程序错误可能导致崩溃。 访问已释放的内存和分配这些错误的最常见*n*字节，然后访问*n*+ 1 个字节。

若要检测的内存损坏，驱动程序验证程序可以通过特殊的池分配驱动程序的内存和监视不当访问该池。 特殊池提供的支持内核模式系统提供的例程，如[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520) ，另外还用于的 GDI 系统提供的例程，如[ **EngAllocMem**](https://msdn.microsoft.com/library/windows/hardware/ff564176)。

两个特殊的池的对齐方式，可使用。 **验证最终**对齐方式是更好地检测访问溢出并**验证启动**对齐方式是更好地检测访问权限不足。 （请注意，大多数的内存损坏问题是由于溢出、 未不足。）

特殊池功能处于活动状态时，**验证结束**已被选择，每个内存分配请求的驱动程序放置在单独的页面。 返回允许的分配页容纳的最高可能的地址，以便与页的最终对齐的内存。 此页面的前面部分编写的特殊的模式。 前一页和下一步页将标记为不可访问。

如果驱动程序将尝试访问的内存分配结束后，驱动程序验证程序将立即检测到这，并将颁发[ **Bug 检查 0xcd 填充**](https://msdn.microsoft.com/library/windows/hardware/ff560219)。 如果该驱动程序写入缓冲区的开头之前内存中，此操作将 （可能） 更改模式。 当释放缓冲区时，驱动程序验证程序将检测更改类型和问题[ **Bug 检查 0xC1**](https://msdn.microsoft.com/library/windows/hardware/ff560183)。

如果该驱动程序读取或写入缓冲区释放后，将发出 Driver Verifier [ **Bug 检查 0xCC**](https://msdn.microsoft.com/library/windows/hardware/ff560216)。

当**验证启动**是选择，网页的开头与对齐的内存缓冲区。 使用此设置，不足会导致立即 bug 检查和释放内存时，溢出会导致的 bug 检查。 此选项在其他方面与**验证结束**选项。

**验证结束**是默认的对齐方式，因为溢出错误是在驱动程序中更常见比不足错误。

单个内存分配可以重写这些设置并选择自己的对齐方式，通过调用[ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)与*优先级*参数集到 XxxSpecialPoolOverrun 或 XxxSpecialPoolUnderrun。 （此例程无法激活或停用特殊的池功能或请求的内存分配，否则将从正常的池分配了特殊池。 仅对齐方式可从控制此例程。）

在 Windows 7 和更高版本的 Windows 操作系统中，特殊池选项支持使用以下内核 Api 分配的内存：

-   [**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)

-   [**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)和其他例程可以分配 I/O 请求数据包 (IRP) 数据结构

-   [**RtlAnsiStringToUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561729)和其他运行时库 (RTL) 的字符串例程

-   [**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)

### <a name="span-idspecialpoolbypooltagorallocationsizespanspan-idspecialpoolbypooltagorallocationsizespanspecial-pool-by-pool-tag-or-allocation-size"></a><span id="special_pool_by_pool_tag_or_allocation_size"></span><span id="SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>特殊的池的池标记或分配大小

这可以驱动程序验证程序的特殊池功能，除了来请求通过指定特殊池分配*驱动程序*，有两种方法可使用特殊的池：

-   **池标记。** 请求所有分配，则使用指定的池标记的特殊的池。

-   **大小。** 请求指定的大小范围内的所有分配的特殊池。

若要请求特殊池为池标记或大小范围，使用 Gflags、 中包含的工具*有关 Windows 调试工具*。 有关详细信息，请参阅[使用 Global Flags Utility](using-the-global-flags-utility.md)。

可以在同一时间使用驱动程序验证程序的特殊池功能和 Gflags 的特殊池功能。 如果这样做，请记住特殊池限制，并非所有尝试从特殊池会成功，并且 Windows 返回成功状态的失败尝试分配特殊池中满足从常规内存分配的分配池。

### <a name="span-idspecialpoolefficiencyspanspan-idspecialpoolefficiencyspanspecial-pool-efficiency"></a><span id="special_pool_efficiency"></span><span id="SPECIAL_POOL_EFFICIENCY"></span>特殊池效率

并非所有特殊池请求完成。 从特殊池中每个分配使用一页的分页物理内存和虚拟地址空间的两个页面。 如果池已用尽，直到再次变为可用的特殊池以标准方式分配内存。 从标准池中填充特殊池请求后发出请求的函数不返回错误，因为在池的请求成功。 因此，不建议如果激活特殊池功能，同时验证多个驱动程序。

发出许多小的内存请求的单个驱动程序还可能会耗尽此池。 如果发生这种情况，可能会更可取的方法将池标记分配给驱动程序的内存分配和一次将特殊池专用于一个池标记。

特殊的池的大小而增加系统; 上的物理内存量理想情况下，这应至少为 1 千兆字节 (GB)。 在 x86 计算机，因为使用虚拟的 （除了为物理） 空间，不使用[ **/3GB** ](https://msdn.microsoft.com/library/windows/hardware/ff556232)启动选项。 它也是最好的两个或三倍增加页面文件的最小/最大数量。

若要确保所有的驱动程序的分配都要经过测试，压力过大，驱动程序，很长的时间段被建议。

### <a name="span-idmonitoringthespecialpoolspanspan-idmonitoringthespecialpoolspanmonitoring-the-special-pool"></a><span id="monitoring_the_special_pool"></span><span id="MONITORING_THE_SPECIAL_POOL"></span>监视特殊池

可以监视与池分配相关的统计信息。 这些可以显示由驱动程序验证程序管理器，Verifier.exe 命令行中，或日志文件中。 请参阅[监视全局计数器](monitoring-global-counters.md)有关详细信息。

如果**池分配成功特殊池中**计数器等于**池分配成功**计数器，则特殊池不足以涵盖所有内存分配。 如果以前计数器低于后者，然后特殊池已耗尽至少一次。

这些计数器不跟踪其大小是一页的分配或更大，因为特殊的池不是适用于它们。

如果启用了特殊池功能，但从特殊的池已分配给不超过 95%的池的所有分配，驱动程序验证程序管理器中，将显示警告。 在 Windows 2000 中，会出现此警告上**驱动程序状态**屏幕。 在 Windows XP 及更高版本，此警告将显示在**全局计数器**屏幕。 如果发生这种情况，应验证驱动程序的短列表，按池标记验证各个池或向系统添加更多的物理内存。

内核调试器扩展 **！ verifier**还可用于监视特殊池使用情况。 它提供类似的驱动程序验证程序管理器的信息。 有关调试器扩展的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的特殊池功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

**请注意**  池标记或分配的大小来激活特殊池功能或设置**验证启动**（检测不足） 和**验证结束**（检测溢出） 对齐方式，使用[全局标志实用工具](using-the-global-flags-utility.md); 这些对齐方式设置适用于所有特殊池分配。

 

-   **在命令行**

    在命令行中，由表示特殊池选项**位 0 (0x1)**。 若要激活特殊的池，使用 0x1 标志值，或将 0x1 添加到标志值。 例如：

    ```
    verifier /flags 0x1 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows 2000 和更高版本的 Windows，您可以还激活和停特殊池用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x1 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    特殊池功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    2.  选择**从完整的列表中选择单个设置**。
    3.  选择 （选中）**特殊池**。

    特殊池功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





