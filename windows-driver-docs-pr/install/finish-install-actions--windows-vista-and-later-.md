---
title: Finish-Install 操作
description: Finish-Install 操作
ms.assetid: 52c7f166-ee74-46b6-815b-5d360d829b4c
keywords:
- 完成安装操作 WDK 设备安装
- 安装程序完成安装操作 WDK 设备安装
- 完成安装向导页 WDK 设备安装
- 类安装程序 WDK 设备安装，完成安装操作
- 共同安装程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e36609faad21bb34165f91c64eb58822506c4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577544"
---
# <a name="finish-install-actions"></a>Finish-Install 操作


**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

*完成安装操作*允许安装程序以完成安装操作。

安装程序可以指定要执行类安装程序、 类共同安装程序或设备共同安装程序，启动 Windows Vista 和更高版本中的完成安装操作。 完成安装操作的管理员上下文中运行*后*完成所有其他安装操作，包括完成安装向导页。

在 Windows 7 中，默认值完成安装操作提供的系统提供[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)函数。 此函数的管理员，交互式上下文中处理[RunOnce 注册表项](runonce-registry-key.md)的设备设置。 如果设备不具有类安装程序中，或类安装程序在响应中返回 ERROR_DI_DO_DEFAULT [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)请求时，Windows 调用**SetupDiFinishInstallAction**设备的所有安装程序完成其完成安装操作后。

在 Windows 8 和更高版本中，完成安装操作将不会自动运行设备安装的一部分并[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)函数已移除。 相反，管理员 （或可以提供管理员凭据对 UAC 提示的受限的用户） 必须转到操作中心并解决在完成安装操作要运行的顺序中的"完成安装设备软件"维护项。 在此之前，完成安装操作将不运行。 例如，如果用户插入设备安装的驱动程序，包括完成安装操作，完成安装操作将不会自动在该时间运行。 相反，完成安装操作将在以后某个时刻时运行用户手动启动它。 此后，Windows 运行时完成安装操作，操作都有该单个机会运行。 如果此操作将失败，它必须采取适当措施来允许用户以重试并完成更高版本。 同样，安装应附带驱动程序的支持软件仍可以使用完成安装操作，但它也不会安装自动。

或者，具体取决于你的方案，在 Windows 8 和更高版本，你可能能够充分利用新的设备应用程序模型。 有关设备应用程序的详细信息可从[设计出色的硬件体验](https://go.microsoft.com/fwlink/p/?linkid=227833)。

完成安装操作可在以下情况下：

-   若要运行未设计为完成安装向导页的一部分运行的特定于设备的应用程序安装程序。 如果此类安装程序具有其自己的用户界面，使用完成安装操作来安装应用程序提供更好的用户体验。

    例如，假设设备制造商想要安装特定于设备的应用程序除了设备的驱动程序和特定于设备的应用程序具有其自己的安装程序使用其自己的用户界面。 若要提供最佳用户体验，设备制造商会以完成安装操作的形式运行安装程序。 这样一来，当 Windows 检测到设备，并找到该驱动程序，Windows 会先安装该驱动程序，然后运行该应用程序的安装程序。

-   若要运行安装程序仅可在 （客户端安装） 的交互式用户上下文中运行。 例如，通过使用启动此类安装程序**InteractiveInstall**指令[ **INF ControlFlags 部分**](inf-controlflags-section.md)的[驱动程序包的](driver-packages.md)INF 文件。

    **请注意**  从 Windows Vista 开始，此类安装程序无法在运行相同的方式与在早期版本的 Windows 上。 这是因为 Windows Vista 和更高版本的 Windows 不支持的客户端安装中的设备的安装。 但是，此类安装程序可以以完成安装操作的形式运行如果驱动程序包包含安装程序类、 类共同安装程序或设备的共同安装程序会启动安装程序。

     

本部分讨论了更详细地完成安装操作，包括以下主题：

[完成安装操作概述](overview-of-finish-install-actions.md)

[实现完成安装操作](implementing-finish-install-actions.md)

[如何处理完成安装操作](how-finish-install-actions-are-processed.md)

 

 





