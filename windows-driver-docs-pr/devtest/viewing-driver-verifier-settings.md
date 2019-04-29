---
title: 查看驱动程序验证程序设置
description: 查看驱动程序验证程序设置
ms.assetid: 2dd5f1b4-5c78-459c-8b73-c8d511f8a22b
keywords:
- 驱动程序验证程序 WDK，查看设置
- 查看驱动程序验证程序设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 113971bef0be1169081c2dda7d2485dab1d43f5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379868"
---
# <a name="viewing-driver-verifier-settings"></a>查看驱动程序验证程序设置


## <span id="ddk_viewing_driver_verifier_settings_tools"></span><span id="DDK_VIEWING_DRIVER_VERIFIER_SETTINGS_TOOLS"></span>


可以通过使用驱动程序验证程序管理器显示当前的驱动程序验证程序设置。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。 在 Windows XP 及更高版本，在这些设置，也可以通过使用显示[**验证程序命令行**](verifier-command-line.md)。

以下方法将显示在下一次启动后才能生效的设置。 其中将包括已选择的驱动程序列表以及要验证的 Driver Verifier 选项的列表。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

(Windows XP 及更高版本)若要显示的驱动程序验证程序设置，请使用**verifier /querysettings**命令。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证程序管理器 (Windows 2000)

若要显示的驱动程序验证程序设置，请选择**设置**选项卡。

按**退出**停止查看这些设置。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证程序管理器 (Windows XP 及更高版本)

若要显示的驱动程序验证程序设置，请启动驱动程序验证程序管理器，并选择**显示现有设置**任务。 然后按**下一步**。

按**完成**停止查看这些设置。

### <a name="span-idviewingthecurrentlyactivefeaturesspanspan-idviewingthecurrentlyactivefeaturesspanviewing-the-currently-active-features"></a><span id="viewing_the_currently_active_features"></span><span id="VIEWING_THE_CURRENTLY_ACTIVE_FEATURES"></span>查看当前使用的功能

如果想要查看的驱动程序验证程序功能当前处于活动状态，而不是将在下一步启动之后，才会生效的设置看到[使用易失性设置](using-volatile-settings.md)。

 

 





