---
title: 选择驱动程序验证程序选项
description: 选择驱动程序验证程序选项
ms.assetid: 02ef5dd6-7532-4979-b45c-a9ee81582788
keywords:
- 驱动程序验证程序 WDK，选项选择
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b0fd151576001898b1d1dce5f8658f855dce27
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351213"
---
# <a name="selecting-driver-verifier-options"></a>选择驱动程序验证程序选项


## <span id="ddk_selecting_driver_verifier_options_tools"></span><span id="DDK_SELECTING_DRIVER_VERIFIER_OPTIONS_TOOLS"></span>


Driver Verifier 选项可以通过使用所选[**验证程序命令行**](verifier-command-line.md)，或通过使用驱动程序验证程序管理器。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要激活或停用的各个选项，指定所需的选项后 **/flags**参数。

(仅适用于 Windows 2000)若要控制的 I/O 验证级别，使用 **/iolevel**参数。

(Windows XP 及更高版本)若要激活的标准选项-[特殊池](special-pool.md)，[强制 IRQL 检查](force-irql-checking.md)，[池跟踪](pool-tracking.md)， [I/O 验证](i-o-verification.md)， [DMA 验证](dma-verification.md)，并[死锁检测](deadlock-detection.md)-使用 **/标准**参数。 从 Windows Vista 开始，标准选项还包括[安全检查](security-checks.md)并[杂项检查](miscellaneous-checks.md)。 从 Windows 8 开始，标准选项还包括[DDI 符合性检查](ddi-compliance-checking.md)。

(Windows Server 2003 及更高版本)若要激活[磁盘完整性检查](disk-integrity-checking.md)，使用 **/磁盘**参数。

若要停用所有选项并清除已验证的驱动程序列表，请使用 **/重置**参数。

请参阅[**验证程序命令行**](verifier-command-line.md)有关详细信息。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证程序管理器 (Windows 2000)

若要激活或停用的各个选项，请选择**设置**选项卡。Driver Verifier 选项所示**验证类型**部分 ([特殊池](special-pool.md)，[强制 IRQL 检查](force-irql-checking.md)，[低资源模拟](low-resources-simulation.md)，[池跟踪](pool-tracking.md)，和[I/O 验证](i-o-verification.md))。 检查想要停用你想要激活，并清除任何选项。 如果选择的 I/O 验证，则可以选择级别 1 和级别 2 （选择级别 2 将启用级别 1 和级别 2 测试）。 若要选择你想要验证的驱动程序，请参阅[选择驱动程序，以验证](selecting-drivers-to-be-verified.md)。

若要启用标准选项--[特殊池](special-pool.md)，[强制 IRQL 检查](force-irql-checking.md)，[池跟踪](pool-tracking.md)，并[I/O 验证](i-o-verification.md)级别 2--选择**设置**选项卡。按**首选设置**按钮。 此外将选择此按钮**验证是否所有驱动程序**选项按钮。 如果你想要现在更改验证驱动程序的列表，请参阅[选择驱动程序，以验证](selecting-drivers-to-be-verified.md); 否则为按**应用**。

若要停用所有选项并清除已验证的驱动程序列表中，选择**设置**选项卡。按**全部重置**按钮。 然后按**应用**。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证程序管理器 (Windows XP 及更高版本)

在 Windows XP 及更高版本，驱动程序验证程序管理器可以多种方式选择选项：

-   若要控制哪些选项完全处于活动状态，请选择**创建自定义设置**任务，然后按**下一步**。 在下一个屏幕上，选择**从完整的列表中选择单个设置**，然后按**下一步**。 下一屏幕中列出的所有驱动程序验证程序的选项 （特殊的池、 池跟踪、 强制 IRQL 检查、 I/O 验证、 增强的 I/O 验证、 死锁检测，DMA 验证和低资源模拟-以及在 Windows 中的磁盘完整性检查Server 2003 及更高版本)。 从 Windows Vista 开始，这些选项还包括[安全检查](security-checks.md)并[杂项检查](miscellaneous-checks.md)。 从 Windows 8 开始，这些选项还包括[电源框架延迟模糊](concurrency-stress-test.md)， [DDI 符合性检查](ddi-compliance-checking.md)， [MDL 堆栈检查固定](invariant-mdl-checking-for-stack.md)，以及[固定 MDL 驱动程序检查](invariant-mdl-checking-for-driver.md)。 从 Windows 8.1 开始，这些选项还包括[NDIS/WIFI 验证](ndis-wifi-verification.md)，[内核同步延迟模糊](kernel-synchronization-delay-fuzzing.md)， [VM 交换机验证](vm-switch-verification.md)，以及[系统资源不足模拟](systematic-low-resource-simulation.md)。 请检查你想要激活任何选项。

-   若要选择从预定义的选项集，请选择**创建自定义设置**任务，然后按**下一步**。 在下一个屏幕上，选择**启用预定义设置**，并选择任何复选框。 选择**标准设置**支持特殊的池、 强制 IRQL 检查、 池跟踪、 I/O 验证、 DMA 验证和死锁检测。 从 Windows Vista 开始，选择标准选项还允许[安全检查](security-checks.md)并[杂项检查](miscellaneous-checks.md)。 从 Windows 8 开始，选择标准选项还允许[DDI 符合性检查](ddi-compliance-checking.md)。 选择**较低的资源模拟**复选框使低资源模拟。 选择**增强的 I/O 验证**复选框启用增强的 I/O 验证。 在 Windows Server 2003 及更高版本中，选择**磁盘完整性检查**复选框使磁盘完整性检查。

-   若要选择的标准选项，请选择**创建标准设置**任务。 标准设置包括特殊池、 强制 IRQL 检查、 池跟踪、 I/O 验证、 DMA 验证和死锁检测。 从 Windows Vista 开始，标准设置还包括[安全检查](security-checks.md)并[杂项检查](miscellaneous-checks.md)。 从 Windows 8 开始，标准设置还包括[DDI 符合性检查](ddi-compliance-checking.md)。

请注意，自 Windows vista 中，如果**较低的资源模拟**使用上面列出的前两个方法之一选择复选框后下, 一个屏幕是用于设置概率、 应用程序、 池标记的屏幕和低资源模拟系统启动延迟时间选项。 这些选项设为所需的值。

完成以下步骤之一操作后，按**下一步**。 请参阅[选择驱动程序，以验证](selecting-drivers-to-be-verified.md)下一步。

若要停用所有选项并清除已验证的驱动程序列表中，选择**删除现有设置**任务。 然后按**完成**。

### <a name="span-idrebootrequiredspanspan-idrebootrequiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>需要重启

从 Windows Vista 开始，可以激活和停用无需重新启动 （"重新启动"） 的所有选项的计算机除外[DDI 符合性检查](ddi-compliance-checking.md)，[电源框架延迟模糊](concurrency-stress-test.md)， [Storport 验证](dv-storport-verification.md)，或[SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

在 Windows Vista 之前的系统，可以激活和停某些选项用不重启，但仅在启用驱动程序验证程序后至少一个驱动程序然后重新启动计算机。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

 

 





