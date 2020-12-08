---
title: 查看驱动程序验证程序设置
description: 查看驱动程序验证程序设置
keywords:
- 驱动程序验证程序 WDK，查看设置
- 查看驱动程序验证程序设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ac66ec4c4d9781a24b7196d48bacb244dfe0dcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815125"
---
# <a name="viewing-driver-verifier-settings"></a>查看驱动程序验证程序设置


## <span id="ddk_viewing_driver_verifier_settings_tools"></span><span id="DDK_VIEWING_DRIVER_VERIFIER_SETTINGS_TOOLS"></span>


使用驱动程序验证器管理器可以显示当前的驱动程序验证程序设置。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。 在 Windows XP 和更高版本中，还可以通过使用验证程序 [**命令行**](verifier-command-line.md)显示这些设置。

下面的方法将显示将在下一次启动后生效的设置。 其中包括已选择的驱动程序验证程序选项列表以及要验证的驱动程序列表。

### <a name="span-idverifier_command_linespanspan-idverifier_command_linespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

 (Windows XP 和更高版本中) 显示驱动程序验证程序设置，请使用 **Verifier/querysettings** 命令。

### <a name="span-iddriver_verifier_manager__windows_2000_spanspan-iddriver_verifier_manager__windows_2000_spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证器管理器 (Windows 2000) 

若要显示 Driver Verifier 设置，请选择 " **设置** " 选项卡。

按 " **退出** " 以停止查看这些设置。

### <a name="span-iddriver_verifier_manager__windows_xp_and_later_spanspan-iddriver_verifier_manager__windows_xp_and_later_spandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证器管理器 (Windows XP 和更高版本) 

若要显示 Driver Verifier 设置，请启动驱动程序验证器管理器并选择 " **显示现有设置** " 任务。 然后按 " **下一步**"。

按 " **完成** " 停止查看这些设置。

### <a name="span-idviewing_the_currently_active_featuresspanspan-idviewing_the_currently_active_featuresspanviewing-the-currently-active-features"></a><span id="viewing_the_currently_active_features"></span><span id="VIEWING_THE_CURRENTLY_ACTIVE_FEATURES"></span>查看 Currently-Active 功能

如果你想要查看当前活动的驱动程序验证程序功能，而不是要在下次启动后生效的设置，请参阅 [使用可变设置](using-volatile-settings.md)。

 

 





