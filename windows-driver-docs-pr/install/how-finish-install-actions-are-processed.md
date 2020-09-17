---
title: 如何处理 Finish-Install 操作
description: 如何处理 Finish-Install 操作
ms.assetid: 028cce46-018d-496e-bc99-c8bf6158c898
keywords:
- 完成-安装操作 WDK 设备安装
- 默认完成-安装操作
- 服务器端安装 WDK
- CONFIG_FINISHINSTALL
- 操作 WDK 完成-安装
- DI_FLAGSEX_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296022ded0d3e9108996c4cb50e22084700f1bfb
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717010"
---
# <a name="how-finish-install-actions-are-processed"></a>如何处理 Finish-Install 操作


完成-设备的安装操作的处理方式与 *安装程序* (类安装程序相同。类共同安装程序或设备共同安装程序) ，无论安装是 [*硬件首次安装*](hardware-first-installation.md) ，还是通过运行安装程序（例如 "找到新硬件向导"、"更新驱动程序软件向导" 或供应商提供的安装程序）启动安装， ([*软件优先安装*](software-first-installation.md)) 。

**注意**   在 Windows 8、Windows 8.1 和 Windows 10 中，必须由管理员 (或可向 UAC 提示符) 提供管理员凭据的受限用户在操作中心完成安装操作。 用户必须单击 "完成安装设备软件"。

 

Windows 进程完成-在所有其他安装操作完成并且设备已启动之后安装操作，包括：

-   核心设备安装 (也称为 *服务器端安装*) ，在这种安装中，系统的即插即用 (PnP) manager 组件安装并加载了设备驱动程序。

Windows 完成了以下步骤来处理安装程序的完成安装操作：

1.  核心设备安装结束时，Windows 将调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 将 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求发送到设备的安装程序。

    DIF_NEWDEVICEWIZARD_FINISHINSTALL 是在核心设备安装环境和客户端上下文中都发送的唯一 DIF 代码。 因此，类安装程序、类共同安装程序或设备共同安装程序必须指示在 DIF_NEWDEVICEWIZARD_FINISHINSTALL 处理期间（而不是在 DIF_INSTALLDEVICE 处理期间）具有完成安装操作。

2.  如果安装程序提供了完成安装操作，则会将 DIF_FLAGSEX_FINISHINSTALL_ACTION 标志设置为响应 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求。 如果在所有安装程序都已处理 DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求后设置了 DIF_FLAGSEX_FINISHINSTALL_ACTION 标志，则将对设备进行标记以执行 "完成安装" 操作。

    有关此操作的详细信息，请参阅将 [设备标记为具有完成安装操作要执行的操作](setting-the-configflag-finishinstall-action-device-configuration-flag.md)。

3.  设备的核心设备安装完成后，Windows 会检查设备是否已标记为执行完成安装操作。 如果有，Windows 将对完成安装过程进行排队，该过程将执行特定于设备的完成安装操作。 此过程在用户的上下文中执行。

    在 Windows 8 及更高版本中，"完成-安装" 操作不会在设备安装过程中自动运行。 相反，管理员 (或可以向 UAC 提示符提供管理员凭据) 的受限用户必须转到操作中心，并解决 "完成安装" 操作要运行的 "完成安装设备软件" 维护项目的要求。 在此之前，"完成-安装" 操作将不会运行。 例如，如果用户插入安装包含 "完成安装" 操作的驱动程序的设备，则 "完成-安装" 操作将不会在该时间自动运行。 "完成-安装" 操作在用户手动启动时运行。 当 Windows 运行 "完成-安装" 操作时，该操作具有运行的单一机会。 如果操作失败，则必须采取适当的措施来允许用户重试并稍后完成。 仍可使用 "完成-安装" 操作来安装应随附驱动程序的支持软件，但它也不会自动安装。

    在 Windows 7 中，仅在以下时间之一使用管理员凭据在用户的上下文中运行完成安装过程：

    -   下一次在附加设备时具有管理员凭据的用户登录的时间。
    -   重新附加设备时。
    -   当用户在设备管理器中选择 " **扫描硬件更改** " 时。

    如果用户在没有管理权限的情况下登录，则 Windows 将提示用户提供许可和凭据，以便在管理员上下文中运行完成安装操作。

4.  当完成安装操作运行时，完成安装过程将启动并完成设备的任何完成安装向导页面，然后调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 将 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求发送到设备的所有安装程序，如 [运行 "完成-安装" 操作](running-finish-install-actions.md)中所述。

5.  安装程序完成其完成安装操作后，Windows 将运行默认的 "完成安装" 操作，如 [运行默认的 "完成安装" 操作](running-the-default-finish-install-action.md)中所述。

 

