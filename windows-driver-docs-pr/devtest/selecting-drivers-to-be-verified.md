---
title: 选择要验证的驱动程序
description: 选择要验证的驱动程序
keywords:
- 驱动程序验证程序 WDK，驱动程序选择
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09caccbe67aa076a676b10b90242b1967e1d89f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799763"
---
# <a name="selecting-drivers-to-be-verified"></a>选择要验证的驱动程序


## <span id="ddk_selecting_drivers_to_be_verified_tools"></span><span id="DDK_SELECTING_DRIVERS_TO_BE_VERIFIED_TOOLS"></span>


可以通过使用 [**验证程序命令行**](verifier-command-line.md)或使用驱动程序验证器管理器来选择要验证的驱动程序。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。

### <a name="span-idverifier_command_linespanspan-idverifier_command_linespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要验证所有驱动程序，请使用 **/all** 参数。

若要验证驱动程序列表，请使用 **/driver** 参数。

有关详细信息，请参阅 [**Verifier 命令行**](verifier-command-line.md) 。

### <a name="span-iddriver_verifier_manager__windows_2000_spanspan-iddriver_verifier_manager__windows_2000_spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证器管理器 (Windows 2000) 

若要验证所有驱动程序，请选择 " **设置** " 选项卡。选择 " **验证所有驱动程序**"。 然后按 " **应用**"。

若要验证驱动程序列表，请选择 " **设置** " 选项卡。选择 " **验证选定的驱动程序**"。 你将看到在最近一次启动时系统中加载的所有驱动程序的列表。

" **验证状态** " 列提供每个驱动程序的当前状态。 可能的 **验证状态** 值为：

<span id="Enabled"></span><span id="enabled"></span><span id="ENABLED"></span>**能够**  
当前正在验证驱动程序，在重新启动后将继续进行验证。

<span id="Disabled"></span><span id="disabled"></span><span id="DISABLED"></span>**Disabled**  
当前未验证驱动程序，重新启动后将不进行验证。

<span id="Enabled__Reboot_Needed_"></span><span id="enabled__reboot_needed_"></span><span id="ENABLED__REBOOT_NEEDED_"></span>**已启用 (需要重启)**  
当前未验证驱动程序，但用户已请求验证此驱动程序。 重新启动后，将验证此驱动程序。

<span id="Disabled__Reboot_Needed_"></span><span id="disabled__reboot_needed_"></span><span id="DISABLED__REBOOT_NEEDED_"></span>**已禁用 (需要重新启动)**  
当前正在验证驱动程序，但用户已请求端进行此验证。 重新启动后，将无法再验证此驱动程序。

你可以从此列表中选择一个或多个驱动程序，然后单击 " **验证** " 或 " **不验证** " 按钮。 你还可以右键单击驱动程序的名称，然后从菜单中进行控制验证。

" **下次重新启动之后验证这些其他驱动程序** " 文本框允许你输入当前未在系统上加载的驱动程序的名称。 必须用空格分隔多个名称。

选择要验证的驱动程序后，按 " **应用**"。

若要停用所有选项并清除 "已验证驱动程序" 列表，请选择 " **设置** " 选项卡。按 " **全部重置** " 按钮。 然后按 " **应用**"。

### <a name="span-iddriver_verifier_manager__windows_xp_and_later_spanspan-iddriver_verifier_manager__windows_xp_and_later_spandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证器管理器 (Windows XP 和更高版本) 

在 Windows XP 和更高版本的驱动程序验证程序管理器中，必须在选择选项之后完成选择驱动程序。 有关第一步的说明，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md) 。

第一步完成后，你将看到 " **选择要验证的驱动程序** " 面板。 可以通过多种方式选择驱动程序：

-   若要验证所有驱动程序，请选择 " **自动选择此计算机上安装的所有驱动程序**"。

-   若要验证驱动程序列表，请选择 " **从列表中选择驱动程序名称** "，然后按 " **下一步**"。 你将看到当前加载的所有驱动程序的列表。  (在 Windows XP 和更高版本中，将不会指示每个驱动程序的当前验证状态。 ) 选中每个要验证的驱动程序旁边的复选框。 若要选择不在列表中的驱动程序，请按 " **添加当前未加载的驱动程序 (s) 到列表**。 这允许你浏览系统中所需的驱动程序文件。 按 " **打开** " 将该驱动程序添加到列表的顶部。 然后，必须选中此驱动程序旁边的复选框以将其选中以供验证。

    从 Windows 8 开始，你可以使用 "驱动程序验证器管理器" 中的按钮来选择所有驱动程序， (**选择所有**) ，清除你的选择 (**取消选择所有**) ，并将选择内容反转 (**反转选择**) 。

-   若要验证未签名的驱动程序，请选择 **自动选择未签名的驱动程序**。 将显示这些驱动程序的列表。  (如果不存在此类驱动程序，将显示一条错误消息。 ) 

-   若要验证为早期版本的 Windows 构建的驱动程序，请选择 " **自动选择为旧版 windows 构建的驱动程序**"。 将显示这些驱动程序的列表。  (如果不存在此类驱动程序，将显示一条错误消息。 ) 

选择要验证的驱动程序后，按 " **下一步** " 或 " **完成**"。

如果启用了磁盘完整性检查，则会显示连接到计算机的所有物理磁盘的列表。 选中要验证的每个磁盘旁边的框，然后按 " **完成**"。

若要停用所有选项并清除 "已验证驱动程序" 列表，请启动驱动程序验证程序管理器，并从第一个屏幕中选择 "**删除现有** 然后按 " **完成**"。

### <a name="span-idreboot_requiredspanspan-idreboot_requiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>需要重新启动

在 Windows XP 和 Windows Server 2003 上，你可以启动和停止对驱动程序的验证，而无需重新启动 ( "重新启动" ) 计算机，但仅当驱动程序未加载时才这样做。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

从 Windows Vista 开始，可以在不重新启动计算机的情况下启动和停止对未加载的驱动程序的验证。 你还可以在不重新启动的情况下，开始验证已加载的驱动程序。 但是，在重新启动系统之前，不能停止对已加载的驱动程序的验证。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

 

 





