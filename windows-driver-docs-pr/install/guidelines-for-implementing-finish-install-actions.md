---
title: 实施 Finish-Install 操作的指南
description: 实施 Finish-Install 操作的指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afa6b12bdc49889bb561c324007f119f36989f06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808133"
---
# <a name="guidelines-for-implementing-finish-install-actions"></a>实施 Finish-Install 操作的指南


完成-安装操作可由 *安装程序* (类安装程序、类共同安装程序或设备共同安装程序) 运行。 在其 "完成安装" 操作中，安装程序可以运行可执行程序、创建进程、创建线程或执行设备驱动程序安装完成-安装过程中的代码。

在安装程序中实现完成安装操作时，请考虑以下准则：

-   完成-不能使用安装操作来应用设备正常运行所需的任何关键设置。

-   如果完成-安装操作必须运行完成，安装程序应等待完成-安装操作完成。

    例如，为了避免在完成安装操作仍在运行时被系统重启中断，安装程序应等待完成-安装操作完成，然后安装程序从处理 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求中返回。

-   "完成-安装" 操作应向用户通知进度。

    Windows 不会通知用户完成-安装操作正在运行，或者完成-安装操作成功或失败。 因此，"完成-安装" 操作应通知用户正在进行 "完成-安装" 操作，然后通知用户完成-安装操作已成功或失败。

-   安装程序必须处理需要重新启动系统才能完成完成安装操作的情况。

    如果在设置在设备上生效之前，"完成-安装" 操作需要重新启动系统，则安装程序在从处理 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求之前，应设置 DI_NEEDREBOOT 标志。 但是，除非绝对必要，否则设备安装不会强制重新启动计算机。

    有关设备安装何时需要重新启动系统的详细信息，请参阅 [设备安装和系统重新](device-installations-and-system-restarts.md)启动。

-   安装程序应处理 "完成-安装" 操作失败的情况，但应再次尝试此操作。 例如，如果要安装的设备已从系统中删除，则安装程序可能会以这种方式使完成安装操作失败。

    在 Windows 8 之前，如果 "完成-安装" 操作失败，但应再次尝试执行，则安装程序应向用户通知临时故障，执行任何必要的清理，并为 DIF_FINISHINSTALL_ACTION 请求返回 Win32 错误代码。 如果安装程序为 DIF_FINISHINSTALL_ACTION 请求返回 Win32 错误代码，则 Windows 不会将设备清除为已标记为对设备节点执行 "完成安装" 操作 (*devnode*) 。

    但是，从 Windows 8 开始，返回错误代码将不会阻止清除标志。 如果 "完成-安装" 操作出错，则需要为用户提供在以后再次运行它的功能。

    虽然此标志仍是为设备设置的，但 Windows 会运行新的完成安装过程。

    有关详细信息，请参阅 [运行 Finish-Install 操作](running-finish-install-actions.md)。

-   安装程序应处理 "完成-安装" 操作失败且不应再次尝试的情况。

    如果错误使完成安装操作无法成功完成，则安装程序应通知用户操作无法完成，然后执行任何必要的清理。 在这种情况下，共同安装程序应返回 NO_ERROR 并且设备或类安装程序应返回 ERROR_DI_DO_DEFAULT。 Windows 随后会将设备清除为已标记为执行 devnode 的 "完成安装" 操作，并调用 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 来执行默认的完成安装操作。

-   当安装程序处理 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 的 DIF 代码时，它应检查是否需要完成安装操作。 如果有必须执行的完成安装操作，则安装程序只应设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志。 如果此标志被设置为不必要的，用户会在重新安装驱动程序的过程中收到额外的设备安装提示，并且 DIF_FINISHINSTALL_ACTION 请求中没有完成安装操作。

    例如，请考虑一个设备共同安装程序，其中 "完成-安装" 操作将安装设备正常运行所需的应用程序。 例如，Microsoft 键盘的 "完成-安装" 操作可能会安装 IntelliType 应用程序。 如果此类共同安装程序处理 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 的 DIF 代码，则应检查是否已安装该应用程序。 如果已安装应用程序，则没有要执行的完成安装操作，因此不应设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志。 在这种情况下，如果联合安装程序错误地设置了 DI_FLAGSEX_FINISHINSTALL_ACTION 标志，则用户将获取不需要的用户帐户控制 (UAC) 即使完成安装操作没有任何要执行的操作也是如此。

    **注意**  从 Windows 7 开始，如果 UAC 设置为默认设置 " (" 当程序尝试对我的计算机进行更改时通知我 ") 或较低的设置时，操作系统将不会在处理完成安装操作时显示具有管理权限的用户的提示。

     

-   在注册实现完成安装操作的安装程序之前，必须在设备的 [INF 文件](overview-of-inf-files.md)的 [**CopyFiles 指令**](inf-copyfiles-directive.md)中包括并安装运行 "完成安装" 操作所需的所有文件。 这是必需的，以便在安装过程中将文件放置在安装程序可访问的位置。

    有关设备或类共同安装程序的注册要求的详细信息，请参阅 [注册类共同安装程序](registering-a-class-co-installer.md)。

 

