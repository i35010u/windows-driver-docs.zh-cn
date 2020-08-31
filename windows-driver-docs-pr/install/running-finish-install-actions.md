---
title: 运行 Finish-Install 操作
description: 运行 Finish-Install 操作
ms.assetid: 9a5f8e7c-ba11-4a2a-82dd-32cd91c3cc39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18db94aefc38a7505b182675f9e300d886671994
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094947"
---
# <a name="running-finish-install-actions"></a>运行 Finish-Install 操作


在 Windows 8 和更高版本的 Windows 中，"完成-安装" 操作不会在设备安装过程中自动运行。 当使用包含 "完成-安装" 操作的驱动程序安装设备时，"完成-安装" 操作不会自动运行。 相反，Windows 会提示用户在 "通知" 区域或 Windows 操作中心中 "完成安装设备软件"。 安装设备软件需要管理员权限。 如果安装失败，则软件必须提示用户再次尝试安装。 仍可使用 "完成-安装" 操作来安装应随附驱动程序的支持软件，但不会自动安装它。

在 Windows 8 之前，如果设备被标记为需要执行 "完成安装" 操作，则 Windows 最初会尝试通过在下列任一时间运行完成安装过程来完成完成安装操作：

-   对于在 Windows 安装过程中安装的设备，在 Windows 安装程序完成后，管理员第一次登录到 Windows 时。

-   对于在安装 Windows 之后安装或重新安装的设备，在核心设备安装操作完成后，如下所示：
    -   对于 [硬件第一次安装](hardware-first-installation.md) 的设备，Windows 将运行初始完成安装过程。 如果当前用户不是管理员，则在运行初始完成安装过程之前，Windows 将首先提示用户输入管理员的凭据。

    -   对于 [软件首次安装](software-first-installation.md) 的设备，Windows 将在启动安装或重新安装的管理员的上下文中运行初始完成安装过程。

在 Windows 8 之前，如果首次尝试完成完成安装操作成功，则完成安装过程会将设备清除为已标记为执行完成安装操作。 如果最初尝试完成 "完成-安装" 操作失败，则完成安装过程不会将设备清除为执行 "完成安装" 操作并退出。 然后，在设备被标记为执行 "完成安装" 操作时，Windows 会反复尝试通过运行新的完成安装过程来完成 "完成-安装" 操作，如下所示：

-   当设备保持安装时，下一次管理员登录时。

-   如果管理员单击设备管理器的 " **操作** " 菜单上的 "扫描硬件更改" 或安装程序将在管理员的上下文中调用 [**CM_Reenumerate_DevNode**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_reenumerate_devnode) 。

如果设备已标记为执行 "完成安装" 操作，则完成安装过程将调用 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 将 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求发送到设备的安装程序。

如果安装程序已完成安装操作，则安装程序将执行 "完成-安装" 操作并返回 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求的相应错误代码。 安装程序返回下表中的错误代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
<td align="left"><p>类安装程序：类安装程序已成功运行其完成安装操作，并请求 Windows 执行其默认处理。</p>
<p>类安装程序还会返回此错误代码（如果它没有完成安装操作）或完成安装操作失败并且不应再次尝试。</p>
<p>设备或类共同安装程序：共同安装程序不会返回此错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>类安装程序：类安装程序已成功运行其完成安装操作。 Windows 不应执行其默认处理。</p>
<p>设备或类共同安装程序：共同安装程序已成功运行其完成安装操作或没有完成安装操作。</p>
<p>如果完成-安装操作失败且不应重试，则共同安装程序也会返回此错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft Win32 错误</p></td>
<td align="left"><p>类安装程序、设备共同安装程序或类共同安装程序在处理完成安装操作时遇到错误，但应尝试再次处理完成安装操作。</p>
<p>通过返回 Win32 错误代码，安装程序会指示 Windows 应运行另一个完成安装过程，以便在下次枚举设备时完成完成安装操作。 安装程序还应告知用户这种情况。</p></td>
</tr>
</tbody>
</table>

 

 

