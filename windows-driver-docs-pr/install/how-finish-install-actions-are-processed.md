---
title: 如何处理完成安装操作
description: 如何处理完成安装操作
ms.assetid: 028cce46-018d-496e-bc99-c8bf6158c898
keywords:
- 完成安装操作 WDK 设备安装
- 默认值完成安装操作
- 服务器端的安装 WDK
- CONFIG_FINISHINSTALL
- WDK 完成安装操作
- DI_FLAGSEX_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e8368607b1af9f00f2a2044cfca3a6dd622ffc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547587"
---
# <a name="how-finish-install-actions-are-processed"></a>如何处理完成安装操作


在通过相同的方式处理设备的完成安装操作*安装程序*（安装程序类、 类共同安装程序中或设备共同安装程序），而不考虑安装是否[ *硬件第一个安装*](hardware-first-installation.md)或通过运行安装程序，如发现新硬件向导、 更新驱动程序软件向导或供应商提供的安装程序 (来启动安装[*软件的第一个安装*](software-first-installation.md))。

**请注意**  在 Windows 8、 Windows 8.1 和 Windows 10 中，完成安装操作必须在操作中心中完成的管理员 （或受限的用户可以提供管理员凭据对 UAC 提示）。 用户必须单击"完成安装设备软件"。

 

Windows 处理完成安装操作后所有其他安装操作已完成，并且设备已开始，包括：

-   核心设备安装 (也称为*服务器端安装*)，而在该设备的驱动程序安装并加载系统的插即用 (PnP) 管理器组件。

Windows 完成以下步骤来处理的安装程序完成安装操作：

1.  在核心设备安装结束时，Windows 将调用[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)发送[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)到设备的安装程序的请求。

    DIF_NEWDEVICEWIZARD_FINISHINSTALL 是这两个上下文中的核心设备安装和客户端上下文中发送的唯一差异代码。 因此，安装程序类、 类共同安装程序或设备共同安装程序必须指示它具有完成安装操作 DIF_NEWDEVICEWIZARD_FINISHINSTALL 在处理期间，而不是在 DIF_INSTALLDEVICE 处理过程。

2.  如果安装程序提供了完成安装操作，则将 DIF_FLAGSEX_FINISHINSTALL_ACTION 标志设置以响应[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)请求。 如果 DIF_FLAGSEX_FINISHINSTALL_ACTION 标志设置的所有安装程序处理完 DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求后，设备将标记执行完成安装操作。

    有关此操作的详细信息，请参阅[将标记为具有执行完成安装操作设备](setting-the-configflag-finishinstall-action-device-configuration-flag.md)。

3.  核心设备安装设备完成后，Windows 将检查设备是否已标记以执行完成安装操作。 如果是，Windows 将排队执行特定于设备的完成安装操作完成安装过程。 在用户的上下文中执行该过程。

    在 Windows 8 和更高版本中，完成安装操作不会自动运行设备安装的一部分。 相反，管理员 （或可以提供管理员凭据对 UAC 提示的受限的用户） 必须转到操作中心并解决要运行的完成安装操作的"完成安装设备软件"维护项。 在此之前，完成安装操作将不运行。 例如，如果用户插入设备安装的驱动程序，包括完成安装操作，完成安装操作将不会自动在该时间运行。 当用户手动启动它时，在以后运行该完成安装操作。 Windows 运行时完成安装操作，操作都有该单个机会运行。 如果此操作将失败，它必须采取适当措施来允许用户以重试并完成更高版本。 安装应附带驱动程序的支持软件仍可以使用完成安装操作，但它也不会安装自动。

    在 Windows 7 中，完成安装过程仅在上下文中运行的具有管理员凭据的用户在以下时间：

    -   具有管理员凭据的用户登录时连接该设备的下一次。
    -   当重新连接设备。
    -   当用户选择**扫描检测硬件改动**设备管理器中。

    如果用户没有管理权限登录，Windows 将提示用户同意的情况下以及凭据才能在管理员上下文中运行的完成安装操作输入。

4.  当完成安装操作的运行，在完成安装过程开始和完成设备，任何完成安装向导页，然后调用[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)发送[ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)中所述对该设备，为所有安装程序的请求[运行完成安装操作](running-finish-install-actions.md)。

5.  安装程序完成其完成安装操作后，Windows 运行默认的完成安装操作，如中所述[运行默认完成安装操作](running-the-default-finish-install-action.md)。

 

 





