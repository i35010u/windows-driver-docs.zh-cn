---
title: 池跟踪
description: 跟踪的池监视器驱动程序进行的内存分配。
ms.assetid: 5b8aa775-d908-4a7a-b54f-6c63ac1ebd13
keywords:
- 内存池跟踪功能 WDK Driver Verifier
- 池跟踪功能 WDK Driver Verifier
- WDK 驱动程序验证程序的内存分配
- WDK 驱动程序验证程序的内存泄漏
- 未释放的内存分配 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8562a9c8ebbc6523376b0c5e64df317b19c8c1e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392079"
---
# <a name="pool-tracking"></a>池跟踪


跟踪的池监视器驱动程序进行的内存分配。 在驱动程序被卸载时，驱动程序验证程序可确保已释放的驱动程序所做的所有分配。

## <span id="ddk_memory_pool_tracking_tools"></span><span id="DDK_MEMORY_POOL_TRACKING_TOOLS"></span>


未释放的内存分配 (也称为*内存泄漏*) 是降低的操作系统性能的一个常见原因。 这些可以片断系统池，并最终导致系统崩溃。

时此选项处于活动状态，驱动程序验证程序将发出错误检查 0xC4 （带有参数 1 等于 0x62) 如果驱动程序卸载不释放所有分配。

如果驱动程序验证程序发出带有参数 1 等于 0x51、 0x52、 0x53、 0x54 或 0x59 此 bug 检查，驱动程序已写入到其分配以外的内存。 在这种情况下，应启用[特殊池](special-pool.md)功能来查找错误的源。

请参阅[ **Bug 检查 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (驱动程序\_VERIFIER\_检测到\_冲突) 的 bug 列表检查参数。

从 Windows Vista 开始，启用池跟踪选项还将启用锁定的页的跟踪。 驱动程序验证程序时此选项处于活动状态，将发出[ **Bug 检查 0xCB** ](https://msdn.microsoft.com/library/windows/hardware/ff560212) (驱动程序\_左侧\_已锁定\_页\_IN\_进程） 如果驱动程序无法在 I/O 操作后释放锁定的页。

在 Windows 7 和更高版本的 Windows 操作系统中，池跟踪选项支持使用以下内核 Api 分配的内存：

-   [**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)

-   [**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)和其他例程可以分配 I/O 请求数据包 (IRP) 数据结构

-   [**RtlAnsiStringToUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561729)和其他运行时库 (RTL) 的字符串例程

-   [**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)

在 Windows 7 和更高版本的 Windows 操作系统中，激活池跟踪时，驱动程序验证工具可以检测尝试分配内核与缓冲池内存*配额*空闲进程的上下文中。 此类尝试通常是指该驱动程序从 DPC 例程中分配内存。 DPC 例程的线程或进程上下文是不可靠，因此尝试收费于该进程的配额不正确。

### <a name="span-idmonitoringpooltrackingspanspan-idmonitoringpooltrackingspanmonitoring-pool-tracking"></a><span id="monitoring_pool_tracking"></span><span id="MONITORING_POOL_TRACKING"></span>监视池跟踪

内存池分配统计信息可以单独监视每个驱动程序正在验证。 由驱动程序验证程序管理器，Verifier.exe 命令行中，或日志文件中，可以显示这些统计信息。 请参阅[监视各个计数器](monitoring-individual-counters.md)有关详细信息。

内核调试器扩展 **！ verifier 0x3**可用于驱动程序被卸载，或在运行跟踪时，驱动程序的当前分配后找到未完成的内存分配。 此扩展还显示了池标记、 对池的大小和每个分配的分配器的地址。 有关调试器扩展的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

### <a name="span-idpoolquotachargesfromdpcroutinespanspan-idpoolquotachargesfromdpcroutinespanspan-idpoolquotachargesfromdpcroutinespanpool-quota-charges-from-dpc-routine"></a><span id="Pool_Quota_Charges_from_DPC_Routine"></span><span id="pool_quota_charges_from_dpc_routine"></span><span id="POOL_QUOTA_CHARGES_FROM_DPC_ROUTINE"></span>从 DPC 例程的池配额费用

内核驱动程序可以调用[ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513)分配内核池内存和分配给当前进程的池配额的字节数进行收费。 驱动程序通常使用直接来自应用程序的请求相关的内存分配的配额。

延迟的过程调用 (DPC) 例程可以在任何进程的上下文中运行。 因此，收费从 DPC 例程的配额将收取随机过程。 更糟糕的是，当 DPC 例程在空闲进程的上下文中运行，这种情况可能会导致内存损坏或系统崩溃。

检测到 Windows 7 中，从开始，Driver Verifier [ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513)来自 DPC 例程的调用。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的池跟踪功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示池跟踪选项**位 3 (0x8)**。 若要激活池跟踪，请使用 0x8 标志值或将 0x8 添加到标志值。 例如：

    ```
    verifier /flags 0x8 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以激活并停用而无需重启计算机，通过添加池跟踪 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x8 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    池跟踪功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中）**池跟踪**。

    池跟踪功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





