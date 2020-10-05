---
title: Finish-Install 操作
description: Finish-Install 操作
ms.assetid: 52c7f166-ee74-46b6-815b-5d360d829b4c
keywords:
- 完成-安装操作 WDK 设备安装
- 安装程序完成-安装操作 WDK 设备安装
- 完成-安装向导页面 WDK 设备安装
- 类安装程序 WDK 设备安装，完成-安装操作
- 共同安装程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2674d3a0af65a22dc64a10ab1253347ec4a94097
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732871"
---
# <a name="finish-install-actions"></a>Finish-Install 操作


**注意**   通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

*完成-安装操作* 允许安装程序完成安装操作。

安装程序可以从 Windows Vista 和更高版本开始，指定类安装程序、类共同安装程序或设备共同安装程序中发生的完成安装操作。 完成-完成所有其他安装操作（包括完成安装向导页） *后* ，在管理员上下文中运行的 "安装操作"。

在 Windows 7 中，默认的 "完成-安装" 操作由系统提供的 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 函数提供。 此函数在管理员的交互上下文中处理为设备设置的 [RunOnce 注册表项](runonce-registry-key.md) 。 如果设备没有类安装程序，或者类安装程序返回 ERROR_DI_DO_DEFAULT 以响应 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求，则 Windows 将在设备的所有安装程序完成其完成安装操作后调用 **SetupDiFinishInstallAction** 。

在 Windows 8 及更高版本中，"完成-安装" 操作不会在设备安装过程中自动运行，并且已删除 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 函数。 相反，管理员 (或可以向 UAC 提示符提供管理员凭据) 的受限用户必须转到操作中心并处理 "完成安装设备软件" 维护项目，才能运行 "完成-安装" 操作。 在此之前，"完成-安装" 操作将不会运行。 例如，如果用户插入安装包含 "完成安装" 操作的驱动程序的设备，则 "完成-安装" 操作将不会在该时间自动运行。 相反，当用户手动启动 "完成-安装" 操作时，将在稍后的某个时间点运行该操作。 此后，当 Windows 运行 "完成-安装" 操作时，该操作将运行该单一机会。 如果操作失败，则必须采取适当的措施来允许用户重试并稍后完成。 同样，还可以使用 "完成-安装" 操作来安装应随附驱动程序的支持软件，但也不会自动安装它。

或者，根据你的方案，在 Windows 8 及更高版本中，你可以使用新的设备应用模型。 有关设备应用的详细信息，请参阅 [设计良好的硬件体验](/windows-hardware/design/)。

完成-安装操作在以下情况下很有用：

-   运行特定于设备的应用程序安装程序，该程序未设计为作为完成安装向导的一部分运行。 如果此类安装程序具有其自己的用户界面，则使用完成安装操作来安装该应用程序可提供更好的用户体验。

    例如，假设设备制造商除了需要安装设备的驱动程序外，还需要安装设备特定的应用程序，并且特定于设备的应用程序具有其自己的用户界面的安装程序。 为了提供最佳的用户体验，设备制造商将运行安装程序作为 "完成-安装" 操作。 这样，当 Windows 检测到设备并找到驱动程序时，Windows 将首先安装驱动程序，然后运行该应用程序的安装程序。

-   若要运行只能在交互式用户上下文中运行的安装程序， (客户端安装) 。 例如，可以通过使用[驱动程序包](driver-packages.md)inf 文件的[**inf ControlFlags 部分**](inf-controlflags-section.md)中的**InteractiveInstall**指令来启动此类安装程序。

    **注意**   从 Windows Vista 开始，此类安装程序无法以与 Windows 早期版本相同的方式运行。 这是因为 Windows Vista 和更高版本的 Windows 不支持在客户端安装中安装设备。 但是，如果驱动程序包包括类安装程序、类共同安装程序或启动安装程序的设备共同安装程序，则此类安装程序可以作为 "完成-安装" 操作运行。

     

本部分更详细地讨论 "完成-安装" 操作，包括以下主题：

[Finish-Install 操作概述](overview-of-finish-install-actions.md)

[实施 Finish-Install 操作](implementing-finish-install-actions.md)

[如何处理 Finish-Install 操作](how-finish-install-actions-are-processed.md)

