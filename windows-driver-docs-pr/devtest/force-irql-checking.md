---
title: 强制 IRQL 检查
description: 强制 IRQL 检查
keywords:
- 强制执行 IRQL 检查功能 WDK 驱动程序验证程序
- IRQL 监视 WDK 驱动程序验证程序
- 旋转锁定 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04b51ead05842565710d26982a0f8eecf53cd304
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839755"
---
# <a name="force-irql-checking"></a>强制 IRQL 检查


## <span id="ddk_forcing_irql_checking_tools"></span><span id="DDK_FORCING_IRQL_CHECKING_TOOLS"></span>


尽管禁止内核模式驱动程序以高 IRQL 访问可分页内存或持有自旋锁，但如果尚未从工作集中对页面进行实际剪裁并将其分页到磁盘，则可能不会注意到此类操作。

当启用强制 IRQL 检查时，驱动程序验证程序为使用系统内存提供极大的压力。 每当要验证的驱动程序请求旋转锁时，将调用 **KeSynchronizeExecution**，或者在调度 \_ 级别或更高的级别引发 IRQL 时，将从工作集中修整包含驱动程序的可分页代码和数据) 的所有系统可分页池、代码和数据 (。 如果驱动程序尝试访问此内存中的任何一个，则驱动程序验证程序会发出 bug 检查。

从 Windows Vista 开始，此选项还会导致驱动程序验证程序在某些同步对象包含在可分页内存中时进行检测。 这些同步对象无法分页，因为操作系统内核正在以提升的 IRQL 访问它们。 驱动程序验证程序可以检测可分页的 [**KTIMER**](../kernel/eprocess.md)、PRKMUTEX、PKSPIN \_ lock、PRKEVENT、PKSPIN \_ LOCK、PRKSEMAPHORE、PERESOURCE 和 [**FAST \_ MUTEX**](../kernel/eprocess.md) 结构。

内存使用量的压力不会直接影响未选择进行验证的驱动程序。 如果未选择用于验证的驱动程序引发 IRQL，则不会触发剪裁操作。 但是，当正在进行验证的驱动程序引发 IRQL 时，驱动程序验证器确实会修整未验证的驱动程序可以使用的页。 因此，当此选项处于活动状态时，有时会捕获未验证的驱动程序提交的错误。

### <a name="span-idmonitoring_irql_raises_and_spin_locksspanspan-idmonitoring_irql_raises_and_spin_locksspanmonitoring-irql-raises-and-spin-locks"></a><span id="monitoring_irql_raises_and_spin_locks"></span><span id="MONITORING_IRQL_RAISES_AND_SPIN_LOCKS"></span>监视 IRQL 引发和旋转锁

可监视 IRQL 引发、旋转锁和对驱动程序所进行的 **KeSynchronizeExecution** 调用的数量。 还可以监视驱动程序验证程序已从工作集中修整可分页内存的次数。 驱动程序验证程序管理器、Verifier.exe 命令行或日志文件可显示这些统计信息。 有关详细信息，请参阅 [监视全局计数器](monitoring-global-counters.md) 。

内核调试器扩展 **！ verifier** 还可用于监视这些统计信息。 它为驱动程序验证器管理器提供了类似的信息。 在 Windows XP 和更高版本中， **！ verifier 0x8** 扩展将显示由正在验证的驱动程序所做的最近 IRQL 更改的日志。 有关调试器扩展的信息，请参阅 [Windows 调试](../debugger/index.md)。

### <a name="span-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespanspan-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespanspan-idcalling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_abovespancalling-keentercriticalregion-or-keleavecriticalregion-at-dispatch_level-or-above"></a><span id="Calling_KeEnterCriticalRegion_or_KeLeaveCriticalRegion_at_DISPATCH_LEVEL_or_Above"></span><span id="calling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_above"></span><span id="CALLING_KEENTERCRITICALREGION_OR_KELEAVECRITICALREGION_AT_DISPATCH_LEVEL_OR_ABOVE"></span>在调度 \_ 级别或更高级别调用 KeEnterCriticalRegion 或 KeLeaveCriticalRegion

[**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 和 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 是一些 api，可用于同步关键驱动程序代码序列的执行，同时提供普通的内核异步过程调用 (apc) 。 不能在 **KeLeaveCriticalRegion** IRQL = 调度 **KeEnterCriticalRegion** \_ 级别或更高级别调用 KeEnterCriticalRegion 和 KeLeaveCriticalRegion api。 在调度级别或更高级别调用 **KeEnterCriticalRegion** 或 **KeLeaveCriticalRegion** \_ 可能会导致系统挂起或内存损坏。

从 Windows 7 开始，如果启用了强制 IRQL 检查选项，则驱动程序验证程序将检测在调度 \_ 级别或更高级别上对这些 api 的调用。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

你可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活强制 IRQL 检查功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，强制 IRQL 检查选项由 **Bit 1 (0x2)** 表示。 若要激活强制 IRQL 检查，请使用标志值0x2 或向标志值添加0x2。 例如：

    ```
    verifier /flags 0x2 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows 2000 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，激活和停用强制执行 IRQL 检查而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x2 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    "强制 IRQL 检查" 功能也包含在标准设置中。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **强制执行 IRQL 检查**。

    "强制 IRQL 检查" 功能也包含在标准设置中。 若要使用此功能，请在驱动程序验证器管理器中单击 " **创建标准设置**"。

 

