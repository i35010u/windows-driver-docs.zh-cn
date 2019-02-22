---
title: 选择要验证驱动程序
description: 选择要验证驱动程序
ms.assetid: a752dea1-f49c-4e58-9e56-6b54701c760e
keywords:
- 驱动程序验证程序 WDK，驱动程序选择
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2eb963341b9012da015bb1151c427d7de5423ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523743"
---
# <a name="selecting-drivers-to-be-verified"></a>选择要验证驱动程序


## <span id="ddk_selecting_drivers_to_be_verified_tools"></span><span id="DDK_SELECTING_DRIVERS_TO_BE_VERIFIED_TOOLS"></span>


驱动程序可以通过选择用于验证[**验证程序命令行**](verifier-command-line.md)，或通过使用驱动程序验证程序管理器。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要验证的所有驱动程序，请使用 **/all**参数。

若要验证驱动程序的列表，请使用 **/driver**参数。

请参阅[**验证程序命令行**](verifier-command-line.md)有关详细信息。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证程序管理器 (Windows 2000)

若要验证的所有驱动程序，请选择**设置**选项卡。选择**验证是否所有驱动程序**。 然后按**应用**。

若要验证驱动程序的列表，请选择**设置**选项卡。选择**验证选定的驱动程序**。 您将看到最新的启动期间加载到系统中的所有驱动程序的列表。

**验证状态**列可为每个驱动程序提供的当前状态。 可能**验证状态**的值为：

<span id="Enabled"></span><span id="enabled"></span><span id="ENABLED"></span>**已启用**  
该驱动程序当前正在验证和验证重启后将继续。

<span id="Disabled"></span><span id="disabled"></span><span id="DISABLED"></span>**已禁用**  
该驱动程序不当前正在验证，并重新启动后不会验证。

<span id="Enabled__Reboot_Needed_"></span><span id="enabled__reboot_needed_"></span><span id="ENABLED__REBOOT_NEEDED_"></span>**已启用 （需要重启）**  
该驱动程序不当前正在验证，但用户已请求此驱动程序验证。 重新启动后，将验证此驱动程序。

<span id="Disabled__Reboot_Needed_"></span><span id="disabled__reboot_needed_"></span><span id="DISABLED__REBOOT_NEEDED_"></span>**已禁用 （需要重启）**  
当前正在验证该驱动程序，但用户已请求此验证结束。 重新启动后，将无法再验证此驱动程序。

可以从此列表中选择一个或多个驱动程序，单击**验证**或**不验证**按钮。 您还可以右键单击驱动程序的名称和从菜单控件验证。

**验证这些其他驱动程序之后下一步重新启动**文本框中，可输入的系统上当前未加载的驱动程序的名称。 必须用空格分隔多个名称。

选择要验证的驱动程序之后, 按**应用**。

若要停用所有选项并清除已验证的驱动程序列表中，选择**设置**选项卡。按**全部重置**按钮。 然后按**应用**。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证程序管理器 (Windows XP 及更高版本)

在 Windows XP 和更高版本的驱动程序验证程序管理器中，选择的驱动程序必须在完成后选择的选项。 请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)有关此第一个步骤的说明。

第一步完成后，您将看到**选择要验证哪些驱动程序**面板。 你可以多种方式选择驱动程序：

-   若要验证的所有驱动程序，请选择**自动选择此计算机上安装的所有驱动程序**。

-   若要验证驱动程序的列表，请选择**从列表中选择驱动程序名称**，然后按**下一步**。 您将看到所有当前加载的驱动程序的列表。 （在 Windows XP 及更高版本，每个驱动程序的当前验证状态不会指示。）检查你想要验证每个驱动程序旁边的框。 若要选择不在列表的驱动程序，按**添加当前未加载到列表的驱动程序**。 这样，您可以浏览到系统的所需的驱动程序文件。 按**打开**该驱动程序添加到列表的顶部。 然后必须检查选择用于验证此驱动程序旁边的框。

    从 Windows 8 开始，你可以使用按钮驱动程序验证程序管理器中选择所有驱动程序 (**全**)，清除所选内容 (**取消全选**)，并反转所选内容 (**反转选择**)。

-   若要验证是否未签名驱动程序，请选择**自动选择未签名驱动程序**。 将显示这些驱动程序的列表。 （如果不存在任何此类驱动程序，一条错误消息将显示。）

-   若要验证内置于早期版本的 Windows 驱动程序，请选择**自动选择内置较旧版本的 Windows 驱动程序**。 将显示这些驱动程序的列表。 （如果不存在任何此类驱动程序，一条错误消息将显示。）

选择要验证的驱动程序后，按任一**下一步**或**完成**。

如果您启用了磁盘完整性检查，将看到附加到您的计算机的所有物理磁盘的列表。 要验证，然后按每个磁盘旁边的复选框**完成**。

若要停用所有选项并清除已验证的驱动程序列表，请启动驱动程序验证程序管理器，并选择**删除现有设置**从第一个屏幕。 然后按**完成**。

### <a name="span-idrebootrequiredspanspan-idrebootrequiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>需要重启

在 Windows XP 和 Windows Server 2003 上，可以启动和停止的驱动程序验证无需重新启动 （"重新启动"） 的计算机，但是仅当未加载该驱动程序。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

从 Windows Vista 开始，可以启动和停止未加载而无需重启计算机的驱动程序的验证。 此外可以启动的驱动程序，而无需重新启动已加载的验证。 但是，不能停止，直到重新启动系统已加载的驱动程序验证。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

 

 





