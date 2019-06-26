---
title: 运行 Finish-Install 操作
description: 运行 Finish-Install 操作
ms.assetid: 9a5f8e7c-ba11-4a2a-82dd-32cd91c3cc39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c152108f561f4779b1a3d53ab9ca53931ca49175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382275"
---
# <a name="running-finish-install-actions"></a>运行 Finish-Install 操作


在 Windows 8 和更高版本的 Windows 中，完成安装操作也不会自动运行设备安装的一部分。 使用包括完成安装操作的驱动程序安装设备时，完成安装操作将不会自动运行。 相反，Windows 将提示用户与"完成安装设备软件"在通知区域中或 Windows 操作中心中。 安装设备软件需要管理员权限。 如果安装失败，该软件必须提示用户再次尝试安装。 安装应附带驱动程序的支持软件仍可以使用完成安装操作，但它将不会自动安装。

Windows 8 之前，如果设备标记为无需执行完成安装操作，Windows 最初将尝试通过在以下时间之一运行完成安装过程完成完成安装操作：

-   在 Windows 安装程序，以管理员身份登录到 Windows 在 Windows 安装完成后的第一个时间期间安装的设备。

-   设备的安装或重新安装之后安装 Windows，核心设备安装操作完成后，按如下所示：
    -   有关[硬件第一个安装](hardware-first-installation.md)的设备，Windows 运行初始完成安装过程。 如果当前用户不是管理员，Windows 将首先提示用户输入的管理员凭据才能运行初始完成安装过程。

    -   有关[软件的第一个安装](software-first-installation.md)的设备，Windows 初始完成安装过程的上下文中运行启动的安装或重新安装的管理员。

Windows 8 之前，如果初始尝试完成的完成安装操作成功，完成安装过程会清除该设备是标记执行完成安装操作。 如果初始尝试完成的完成安装操作失败，在完成安装过程不会清除该设备是被标记为完成安装操作并退出执行。 随后，虽然标记以执行完成，设备保持安装操作，Windows 反复尝试来完成完成安装操作运行新的完成安装进程，只要枚举设备时，按如下所示：

-   尽管该设备仍然会安装下, 一次以管理员身份登录。

-   如果管理员单击扫描硬件更改**操作**菜单上的设备管理器或安装程序将调用[ **CM_Reenumerate_DevNode** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_reenumerate_devnode)上下文中管理员。

如果该设备添加了标志，以执行完成安装操作，完成安装处理调用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)发送[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)到设备的安装程序的请求。

如果安装程序完成安装操作，安装程序执行完成安装操作，并返回相应的错误代码[ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)请求。 安装程序将返回一个错误代码如下表中。

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
<td align="left"><p>安装程序类：类安装程序成功运行其完成安装操作，并正在请求 Windows 执行默认处理。</p>
<p>如果它不包含完成安装操作，或完成安装操作失败，因而不应再次尝试，类安装程序也会返回此错误代码。</p>
<p>设备或类共同安装程序：共同安装程序不会返回此错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>安装程序类：类安装程序已成功运行其完成安装操作。 Windows 不应执行默认处理。</p>
<p>设备或类共同安装程序：辅助安装程序已成功运行其完成安装操作，或者具有未完成安装操作。</p>
<p>如果完成安装操作失败，并且不应再次尝试，辅助安装程序也会返回此错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft Win32 错误</p></td>
<td align="left"><p>类安装程序、 设备共同安装程序或类共同安装程序在处理完成安装操作时遇到错误，但应尝试处理的完成安装操作。</p>
<p>通过返回一个 Win32 错误代码，安装程序指示 Windows 应运行另一个完成安装过程完成下一次枚举设备的完成安装操作。 安装程序还应通知这种情况下的用户。</p></td>
</tr>
</tbody>
</table>

 

 

 





