---
title: 池跟踪
description: 池跟踪监视驱动程序所进行的内存分配。
keywords:
- 内存池跟踪功能 WDK 驱动程序验证程序
- 池跟踪功能 WDK 驱动程序验证程序
- 内存分配 WDK 驱动程序验证程序
- 内存泄漏 WDK 驱动程序验证程序
- unfreed 内存分配 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac83d549b258ccb58f7805a66d07c49852669bc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841031"
---
# <a name="pool-tracking"></a>池跟踪


池跟踪监视驱动程序所进行的内存分配。 卸载驱动程序时，驱动程序验证程序确保已释放驱动程序所做的所有分配。

## <span id="ddk_memory_pool_tracking_tools"></span><span id="DDK_MEMORY_POOL_TRACKING_TOOLS"></span>


Unfreed 内存分配 (也称为 *内存泄漏*) 导致操作系统性能降低的常见原因。 这会使系统池分段并最终导致系统崩溃。

当此选项处于活动状态时，驱动程序验证器将发出 bug 检查 0xC4 (，其中参数1等于 0x62) 如果驱动程序卸载，而不释放其所有分配。

如果驱动程序验证器发出此错误检查，且参数1等于0x51、0x52、0x53、0x54 或0x59，则驱动程序已写入其分配之外的内存。 在这种情况下，应启用 " [特殊池](special-pool.md) " 功能以找到错误的源。

有关错误检查参数的列表，请参阅 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序 \_ 验证器 \_ 检测到 \_ 冲突) 。

从 Windows Vista 开始，启用池跟踪选项还可以跟踪锁定的页面。 当此选项处于活动状态时，驱动程序验证器将发出 [**Bug 检查 0xCB**](../debugger/bug-check-0xcb--driver-left-locked-pages-in-process.md) \_ \_ \_ \_ \_ 。如果驱动程序在执行 I/o 操作后未能释放锁定) 的页，则该驱动程序将发出 Bug 检查 (。

在 windows 7 和更高版本的 Windows 操作系统中，池跟踪选项支持使用以下内核 Api 分配的内存：

-   [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

-   [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 以及可以 (IRP) 数据结构分配 i/o 请求包的其他例程

-   [**RtlAnsiStringToUnicodeString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring) 和其他运行时库 (RTL) 字符串例程

-   [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

在 windows 7 和更高版本的 Windows 操作系统中，当池跟踪被激活时，驱动程序验证器可以检测到在空闲进程的上下文中以 *配额* 分配内核池内存的尝试。 此类尝试通常意味着驱动程序正在从 DPC 例程分配内存。 DPC 例程的线程或进程上下文不可靠，因此尝试将配额计费到该进程不正确。

### <a name="span-idmonitoring_pool_trackingspanspan-idmonitoring_pool_trackingspanmonitoring-pool-tracking"></a><span id="monitoring_pool_tracking"></span><span id="MONITORING_POOL_TRACKING"></span>监视池跟踪

可以单独监视每个要验证的驱动程序的内存池分配统计信息。 驱动程序验证程序管理器、Verifier.exe 命令行或日志文件可显示这些统计信息。 有关详细信息，请参阅 [监视各个计数器](monitoring-individual-counters.md) 。

内核调试器扩展 **！ verifier 0x3** 可用于在卸载驱动程序之后查找未完成的内存分配，或在驱动程序运行期间跟踪当前分配。 此扩展还显示池标记、池的大小以及每个分配的分配器的地址。 有关调试器扩展的信息，请参阅 [Windows 调试](../debugger/index.md)。

### <a name="span-idpool_quota_charges_from_dpc_routinespanspan-idpool_quota_charges_from_dpc_routinespanspan-idpool_quota_charges_from_dpc_routinespanpool-quota-charges-from-dpc-routine"></a><span id="Pool_Quota_Charges_from_DPC_Routine"></span><span id="pool_quota_charges_from_dpc_routine"></span><span id="POOL_QUOTA_CHARGES_FROM_DPC_ROUTINE"></span>来自 DPC 例程的池配额费用

内核驱动程序可以调用 [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag) 来分配内核池内存，并收取分配给当前进程的池配额的字节数。 驱动程序通常使用与来自应用程序的请求直接相关的内存分配配额。

延迟的过程调用 (DPC) 例程可以在任何进程的上下文中运行。 因此，来自 DPC 例程的充电配额会为随机过程收取费用。 更糟的是，当 DPC 例程在空闲进程的上下文中运行时，这种情况可能会导致内存损坏或系统崩溃。

从 Windows 7 开始，驱动程序验证程序检测来自 DPC 例程的 [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag) 调用。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

你可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活池跟踪功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，池跟踪选项由 **第3个 (0x8)** 表示。 若要激活池跟踪，请使用值为0x8 的标志值或将0x8 添加到标志值。 例如：

    ```
    verifier /flags 0x8 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，来激活和停用池跟踪，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x8 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    标准设置中也包含池跟踪功能。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **池跟踪**。

    标准设置中也包含池跟踪功能。 若要使用此功能，请在驱动程序验证器管理器中单击 " **创建标准设置**"。

 

