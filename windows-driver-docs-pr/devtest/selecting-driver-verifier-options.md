---
title: 选择驱动程序验证程序选项
description: 选择驱动程序验证程序选项
keywords:
- 驱动程序验证程序 WDK，选项选择
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d29d76839d4f486fb9918f3e8c07619b304a6ded
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786887"
---
# <a name="selecting-driver-verifier-options"></a>选择驱动程序验证程序选项


## <span id="ddk_selecting_driver_verifier_options_tools"></span><span id="DDK_SELECTING_DRIVER_VERIFIER_OPTIONS_TOOLS"></span>


可以通过使用 [**验证程序命令行**](verifier-command-line.md)或使用驱动程序验证器管理器来选择驱动程序验证程序选项。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。

### <a name="span-idverifier_command_linespanspan-idverifier_command_linespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要激活或停用个别选项，请在 **/flags** 参数后指定所需的选项。

 (Windows 2000 仅) 控制 i/o 验证的级别，请使用 **/iolevel** 参数。

 (Windows XP 和更高版本) 激活标准选项-- [特殊池](special-pool.md)、 [强制 IRQL 检查](force-irql-checking.md)、 [池跟踪](pool-tracking.md)、 [I/o 验证](i-o-verification.md)、 [DMA 验证](dma-verification.md)和 [死锁检测](deadlock-detection.md) --使用 **/标准** 参数。 从 Windows Vista 开始，标准选项还包括 [安全检查](security-checks.md) 和 [其他检查](miscellaneous-checks.md)。 从 Windows 8 开始，标准选项还包括 [DDI 相容性检查](ddi-compliance-checking.md)。

 (Windows Server 2003 和更高版本中) 若要激活 [磁盘完整性检查](disk-integrity-checking.md)，请使用 **/disk** 参数。

若要停用所有选项并清除验证的驱动程序列表，请使用 **/reset** 参数。

有关详细信息，请参阅 [**Verifier 命令行**](verifier-command-line.md) 。

### <a name="span-iddriver_verifier_manager__windows_2000_spanspan-iddriver_verifier_manager__windows_2000_spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证器管理器 (Windows 2000) 

若要激活或停用个别选项，请选择 " **设置** " 选项卡。驱动程序验证程序的选项列在 " **验证类型** " 部分 ([特殊池](special-pool.md)"、" [强制 IRQL 检查](force-irql-checking.md)"、" [低资源模拟](low-resources-simulation.md)"、" [池跟踪](pool-tracking.md)"和" i/o [验证](i-o-verification.md) ") 。 检查想要激活的选项，并清除要停用的选项。 如果选择了 "i/o 验证"，则可以在级别1和级别2之间进行选择 (选择 "级别 2" 将同时启用第1级和第2级测试) 。 若要选择要验证的驱动程序，请参阅 [选择要验证的驱动程序](selecting-drivers-to-be-verified.md)。

若要启用标准选项-" [特殊池](special-pool.md)"、 ["强制执行 IRQL 检查](force-irql-checking.md)、 [池跟踪](pool-tracking.md)和 [i/o 验证](i-o-verification.md) 级别 2"，请选择 " **设置** " 选项卡。按首选的 " **设置** " 按钮。 此按钮还选中 " **验证所有驱动程序** " 选项按钮。 如果现在想要更改已验证的驱动程序列表，请参阅 [选择要验证的驱动程序](selecting-drivers-to-be-verified.md);否则，按 " **应用**"。

若要停用所有选项并清除 "已验证驱动程序" 列表，请选择 " **设置** " 选项卡。按 " **全部重置** " 按钮。 然后按 " **应用**"。

### <a name="span-iddriver_verifier_manager__windows_xp_and_later_spanspan-iddriver_verifier_manager__windows_xp_and_later_spandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证器管理器 (Windows XP 和更高版本) 

在 Windows XP 和更高版本中，驱动程序验证器管理器可以通过多种方式选择选项：

-   若要精确控制哪些选项处于活动状态，请选择 " **创建自定义设置** " 任务，然后按 " **下一步**" 在下一个屏幕上，选择 " **从完整列表中选择单个设置**"，然后按 " **下一步**"。 下一屏列出了驱动程序验证程序的所有选项 (特殊池、池跟踪、强制 IRQL 检查、i/o 验证、增强的 i/o 验证、死锁检测、DMA 验证和低资源模拟，以及 Windows Server 2003 和更高版本中的磁盘完整性检查) 。 从 Windows Vista 开始，选项还包括 [安全检查](security-checks.md) 和 [其他检查](miscellaneous-checks.md)。 从 Windows 8 开始，选项还包括 [Power Framework 延迟模糊](concurrency-stress-test.md)处理、 [DDI 相容性检查](ddi-compliance-checking.md)、 [堆栈的固定 mdl 检查](invariant-mdl-checking-for-stack.md)以及 [驱动程序的固定 mdl 检查](invariant-mdl-checking-for-driver.md)。 从 Windows 8.1 开始，选项还包括 [NDIS/WIFI 验证](ndis-wifi-verification.md)、 [内核同步延迟模糊](kernel-synchronization-delay-fuzzing.md)处理、 [VM 交换机验证](vm-switch-verification.md)和 [系统低资源模拟](systematic-low-resource-simulation.md)。 检查想要激活的选项。

-   若要选择预定义的选项集，请选择 " **创建自定义设置** " 任务，然后按 " **下一步**"。 在下一个屏幕上，选择 " **启用预定义设置** " 并选择任意复选框。 选择 **标准设置** 可启用特殊池、强制执行 IRQL 检查、池跟踪、i/o 验证、DMA 验证和死锁检测。 从 Windows Vista 开始，选择标准选项还可以启用 [安全检查](security-checks.md) 和 [其他检查](miscellaneous-checks.md)。 从 Windows 8 开始，选择标准选项还可以启用 [DDI 相容性检查](ddi-compliance-checking.md)。 选中 " **低资源模拟** " 复选框可实现低资源模拟。 选中 " **增强的 I/o 验证** " 复选框可启用增强的 i/o 验证。 在 Windows Server 2003 及更高版本中，选中 **磁盘完整性** 检查复选框可启用磁盘完整性检查。

-   若要选择标准选项，请选择 " **创建标准设置** " 任务。 标准设置包括特殊池、强制 IRQL 检查、池跟踪、i/o 验证、DMA 验证和死锁检测。 从 Windows Vista 开始，标准设置还包括 [安全检查](security-checks.md) 和 [其他检查](miscellaneous-checks.md)。 从 Windows 8 开始，标准设置还包括 [DDI 相容性检查](ddi-compliance-checking.md)。

请注意，从 Windows Vista 开始，如果使用上面列出的前两种方法中的任一方法选中 " **低资源模拟** " 复选框，则下一个屏幕是用于为低资源模拟设置 "概率"、"应用程序"、"池标记" 和 "系统启动延迟时间" 选项的屏幕。 将这些选项设置为所需的值。

完成这些步骤之一后，按 " **下一步**"。 请参阅 [选择要验证的驱动程序以](selecting-drivers-to-be-verified.md) 进行下一步。

若要停用所有选项并清除 "已验证驱动程序" 列表，请选择 " **删除现有设置** " 任务。 然后按 " **完成**"。

### <a name="span-idreboot_requiredspanspan-idreboot_requiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>需要重新启动

从 Windows Vista 开始，你可以激活和停用所有选项，而无需重新启动 ) 计算机上的 ( "重新启动"，但会出现 [DDI 相容性检查](ddi-compliance-checking.md)、 [Power Framework 延迟模糊](concurrency-stress-test.md)、 [Storport 验证](dv-storport-verification.md)或 [SCSI 验证](scsi-verification.md)。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

在 Windows Vista 之前的系统上，你可以在不重新启动的情况下激活和停用某些选项，但只有在至少一个驱动程序上启用了驱动程序验证程序之后，才能重新启动计算机。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

 

 





