---
title: 实施 Finish-Install 操作的指南
description: 实施 Finish-Install 操作的指南
ms.assetid: 455d520a-ccd7-470b-ab5f-5786ee90b91d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b7ed73d15a5e8bde117141ab8b48edcbf5ca040
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355152"
---
# <a name="guidelines-for-implementing-finish-install-actions"></a>实施 Finish-Install 操作的指南


完成安装操作可以通过运行*安装程序*（安装程序类、 类共同安装程序中或设备共同安装程序）。 在其完成安装操作，安装程序可以运行可执行程序、 创建过程、 创建线程，或在设备驱动程序安装完成安装过程中执行代码。

当在安装程序中实现完成安装操作，请考虑以下准则：

-   完成安装操作不能用于应用所需的设备正常工作的任何关键设置。

-   安装程序应等待完成安装操作完成，如果完成安装操作必须运行完毕。

    例如，若要避免完成安装操作仍在运行时，系统重新启动被中断，安装程序应等待完成安装操作完成，然后安装程序将返回从处理[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)请求。

-   完成安装操作应该通知用户进度。

    完成安装操作正在运行或完成安装操作成功或失败，Windows 不会通知用户。 因此，完成安装操作应通知用户完成安装操作正在进行，然后通知的用户的完成安装操作是成功还是失败。

-   安装程序必须处理这种情况，需要重新启动系统才能完成完成安装操作。

    从处理在返回之前，安装程序完成安装操作需要重启系统，在设备上的设置生效之前，如果应设置 DI_NEEDREBOOT 标志[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)请求。 但是，设备安装不应该强制重新启动计算机除非绝对必要。

    详细了解当设备安装应需要系统重新启动，请参阅[设备安装和系统重启](device-installations-and-system-restarts.md)。

-   安装程序应处理的情况： 完成安装操作失败，但应该重试。 例如，如果从系统中删除正在安装的设备安装程序可能会失败这种方式中的完成安装操作。

    Windows 8 之前如果完成安装操作失败，但应该重试，安装程序应通知的临时故障，用户执行任何必要的清理，并返回 DIF_FINISHINSTALL_ACTION 请求的 Win32 错误代码。 如果安装程序返回 DIF_FINISHINSTALL_ACTION 请求的 Win32 错误代码，Windows 将不会清除该设备是具有已标记以完成安装操作执行的设备节点 (*devnode*)。

    但是，从 Windows 8 开始，返回错误代码不会阻止正在清除的标志。 如果完成安装操作中有错误，它需要用户提供可以在以后再次运行。

    为设备设置此标志保持，Windows 将运行新的完成安装过程。

    有关详细信息，请参阅[运行完成安装操作](running-finish-install-actions.md)。

-   安装程序应处理的情况，完成安装操作失败，而不应再次尝试。

    如果某个错误而使不可能曾经要成功完成安装操作，安装程序应通知用户的操作无法完成，以及然后执行任何必要的清理。 在此情况下，辅助安装程序应返回 NO_ERROR 和设备或类安装程序应返回 ERROR_DI_DO_DEFAULT。 Windows 随后将清除该设备是具有已标记以完成安装操作执行 devnode 和调用[ **SetupDiFinishInstallAction** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))执行默认完成安装操作。

-   当安装程序处理[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall) DIF 代码，它应该检查是否需要完成安装的任何操作。 如果必须执行的完成安装操作，安装程序应仅设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志。 如果不必要地设置此标志，用户获得额外的设备安装提示期间重新安装该驱动程序，并且 DIF_FINISHINSTALL_ACTION 请求具有要执行的完成安装操作。

    例如，请考虑在其中完成安装操作将安装应用程序所需的设备才能正常工作的设备共同安装程序。 例如，Microsoft 键盘的完成安装操作可能会安装 IntelliType 应用程序。 当处理此类共同安装程序[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall) DIF 代码，它应检查以查看是否已安装应用程序。 如果已安装应用程序，没有完成安装操作执行，并因此 DI_FLAGSEX_FINISHINSTALL_ACTION 标志不应设置。 在此情况下，如果共同安装程序未正确设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志，用户会收到权限才能继续虽然完成安装操作具有要执行的操作不需要的用户帐户控制 (UAC) 提示。

    **请注意**  如果 UAC 设置为默认设置时通知我"仅当程序尝试对我的计算机进行更改时"） 或较低的设置，从 Windows 7 开始，操作系统不显示与管理用户的提示当处理完成安装操作的权限。

     

-   在注册实现完成安装操作的安装程序之前，必须包括并安装运行完成安装操作所需的所有文件[ **CopyFiles 指令**](inf-copyfiles-directive.md)的[INF 文件](overview-of-inf-files.md)设备。 这是必需的以便将文件放在安装过程中可访问的位置由安装程序。

    有关设备或类共同安装程序的注册要求的详细信息，请参阅[注册类共同安装程序](registering-a-class-co-installer.md)。

 

 





