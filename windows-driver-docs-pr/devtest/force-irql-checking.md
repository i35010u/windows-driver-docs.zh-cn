---
title: 强制 IRQL 检查
description: 强制 IRQL 检查
ms.assetid: cb972a72-6504-4ed7-9618-2830192fda1d
keywords:
- 强制 IRQL 检查功能 WDK Driver Verifier
- 监视 WDK Driver Verifier 的 IRQL
- 旋转锁 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99f565d0983d0abb794c690d315b7a18d21270e4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372696"
---
# <a name="force-irql-checking"></a>强制 IRQL 检查


## <span id="ddk_forcing_irql_checking_tools"></span><span id="DDK_FORCING_IRQL_CHECKING_TOOLS"></span>


尽管内核模式驱动程序禁止访问可分页内存以高 IRQL 或占用自旋锁时，此操作可能不引人注目工作是否页面具有不实际已从裁剪掉设置和分页输出到磁盘。

启用强制 IRQL 检查后，驱动程序验证程序提供的系统内存使用极端的压力。 正在验证的驱动程序请求旋转锁，每当调用**KeSynchronizeExecution**，或引发调度到 IRQL\_级别或更高版本，所有的系统可分页池、 代码和数据 （其中包括在驱动程序删除的工作集的可分页的代码和数据）。 如果尝试访问此内存的任何驱动程序，驱动程序验证程序发出的 bug 检查。

从 Windows Vista 开始，此选项还会导致驱动程序验证程序检测某些同步对象包含可分页内存中时。 不能分页这些同步对象，因为操作系统内核在提升的 IRQL 访问它们。 驱动程序验证工具可以检测可分页[ **KTIMER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)，PRKMUTEX、 PKSPIN\_锁，PRKEVENT，PKSPIN\_锁、 PRKSEMAPHORE、 PERESOURCE，和[ **快速\_MUTEX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。

此内存使用情况的压力不会直接影响没有选择进行验证的驱动程序。 当未选择用于验证的驱动程序引发 IRQL 时，它不会触发修整操作。 但是，当正在被验证的驱动程序引发 IRQL，驱动程序验证程序 does trim 可以使用未验证的驱动程序的页。 使此选项处于活动状态时，可能偶尔会捕获由未验证的驱动程序提交的错误。

### <a name="span-idmonitoringirqlraisesandspinlocksspanspan-idmonitoringirqlraisesandspinlocksspanmonitoring-irql-raises-and-spin-locks"></a><span id="monitoring_irql_raises_and_spin_locks"></span><span id="MONITORING_IRQL_RAISES_AND_SPIN_LOCKS"></span>监视 IRQL 引发和自旋锁

IRQL 引发、 自旋锁和对调用的数量**KeSynchronizeExecution**所做的驱动程序可以监视正在验证。 此外可以监视的驱动程序验证程序具有修整从工作集中的可分页内存的次数。 由驱动程序验证程序管理器，Verifier.exe 命令行中，或日志文件中，可以显示这些统计信息。 请参阅[监视全局计数器](monitoring-global-counters.md)有关详细信息。

内核调试器扩展 **！ verifier**还可用于监视这些统计信息。 它提供类似的驱动程序验证程序管理器的信息。 在 Windows XP 及更高版本， **！ verifier 0x8**扩展将显示最新的 IRQL 所做的更改正在验证的驱动程序日志。 有关调试器扩展的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

### <a name="span-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespanspan-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespanspan-idcallingkeentercriticalregionorkeleavecriticalregionatdispatchlevelorabovespancalling-keentercriticalregion-or-keleavecriticalregion-at-dispatchlevel-or-above"></a><span id="Calling_KeEnterCriticalRegion_or_KeLeaveCriticalRegion_at_DISPATCH_LEVEL_or_Above"></span><span id="calling_keentercriticalregion_or_keleavecriticalregion_at_dispatch_level_or_above"></span><span id="CALLING_KEENTERCRITICALREGION_OR_KELEAVECRITICALREGION_AT_DISPATCH_LEVEL_OR_ABOVE"></span>在调度调用 KeEnterCriticalRegion 或 KeLeaveCriticalRegion\_级别或更高版本

[**KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)并[ **KeLeaveCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion) Api，您可以使用与传送同步的驱动程序代码的关键序列执行普通内核异步过程调用 (Apc)。 **KeEnterCriticalRegion**并**KeLeaveCriticalRegion** Api 不能调用在 IRQL = 调度\_级别或更高版本。 调用**KeEnterCriticalRegion**或**KeLeaveCriticalRegion**在调度\_级别或更高版本可能会导致系统挂起或内存损坏。

从 Windows 7 开始，驱动程序验证程序检测到调用这些 Api 在调度\_级别或更高版本如果启用强制 IRQL 检查选项。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的强制 IRQL 检查功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示强制 IRQL 检查选项**位 1 (0x2)** 。 若要激活强制 IRQL 检查，使用 0x2 标志值，或将 0x2 添加到标志值。 例如：

    ```
    verifier /flags 0x2 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows 2000 和更高版本的 Windows，您可以还激活和停用而无需重启计算机，通过添加的强制 IRQL 检查 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x2 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    强制 IRQL 检查功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **Force IRQL 检查**。

    强制 IRQL 检查功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





