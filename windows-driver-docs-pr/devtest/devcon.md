---
title: Windows 设备控制台 (Devcon.exe)
description: DevCon (Devcon.exe) 设备控制台中，是一个命令行工具，运行 Windows 的计算机上显示有关设备的详细的信息。
ms.assetid: ac74200e-e2ae-40db-9fb7-5ea2e7760613
keywords:
- DevCon WDK
- 设备控制台 WDK
- 驱动程序测试 WDK，DevCon
- 测试驱动程序 WDK，DevCon
- 设备信息 WDK DevCon
- 搜索 WDK DevCon
- 显示设备信息
- 更改设备配置 WDK DevCon
- 操作设备 WDK DevCon
- 状态将更改 WDK DevCon
- 重新启动设备
- 设备管理 WDK DevCon
- 列出 WDK 的设备信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1298d1f2c410bcbeb23989ba44c121d07b129552
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371511"
---
# <a name="windows-device-console-devconexe"></a>Windows 设备控制台 (Devcon.exe)


DevCon (Devcon.exe) 设备控制台中，是一个命令行工具，运行 Windows 的计算机上显示有关设备的详细的信息。 可以使用 DevCon 启用、禁用、安装、配置以及删除设备。

DevCon 在 Microsoft Windows 2000 和更高版本的 Windows 上运行。

## <span id="ddk_devcon_tools"></span><span id="DDK_DEVCON_TOOLS"></span>


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在何处可以下载 DevCon？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在安装 WDK、 Visual Studio 和适用于桌面应用程序的 Windows SDK 时 DevCon (Devcon.exe) 包含。 有关下载工具包的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">下载 Windows 硬件</a>。</p>
<p><strong>Windows Driver Kit (WDK) 8 和 Windows Driver Kit (WDK) 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p>
<p>%WindowsSdkDir%\tools\arm\devcon.exe</p>
<div class="alert">
<strong>请注意</strong>Visual Studio 环境变量，%windowssdkdir%，表示 Windows 工具包工具包安装的目录，例如，C:\Program Files (x86) \Windows Kits\8.1 的路径。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

本部分包括：

[DevCon 命令](devcon-general-commands.md)

[DevCon 示例](devcon-examples.md)

## <a name="span-idwhatyoucandowithdevconspanspan-idwhatyoucandowithdevconspanspan-idwhatyoucandowithdevconspanwhat-you-can-do-with-devcon"></a><span id="What_you_can_do_with_DevCon"></span><span id="what_you_can_do_with_devcon"></span><span id="WHAT_YOU_CAN_DO_WITH_DEVCON"></span>您可以使用 DevCon 做什么


Windows 驱动程序开发人员和测试人员可以使用 DevCon 以验证驱动程序，安装并配置正确，包括正确的 INF 文件、 驱动程序堆栈，驱动程序文件和驱动程序包。 您还可以使用 DevCon 命令 （启用、 禁用、 安装、 启动、 停止和继续） 脚本来测试该驱动程序中。

DevCon 是一个命令行工具，会在本地计算机和远程计算机上执行设备管理功能。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。

 

Devcon 功能包括：

-   **显示驱动程序和设备信息**DevCon 可以显示本地计算机和远程计算机上的驱动程序和设备的下列属性 (运行 Windows XP 及更早版本):
    -   硬件 Id、 兼容 Id 和设备实例 Id。 中详细描述了这些标识符[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。
    -   [设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)
    -   设备安装程序类中的设备
    -   INF 文件和设备驱动程序文件
    -   详细信息[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)
    -   硬件资源
    -   设备状态
    -   预期的驱动程序堆栈
    -   驱动程序存储区中的第三方驱动程序包
-   **搜索设备**DevCon 可以搜索已安装和卸载设备硬件 ID、 设备实例 ID 或设备安装程序类的本地或远程计算机上。

-   **更改设备设置**DevCon 可以按以下方式更改状态或在本地计算机上的插即用 (PnP) 设备的配置：
    -   启用设备
    -   禁用设备
    -   更新驱动程序 （交互式和非交互式）
    -   安装设备 （创建 devnode 和安装软件）
    -   从设备树中删除设备并删除其设备堆栈
    -   重新扫描插设备
    -   添加、 删除和重新排列硬件根枚举设备的 Id
    -   更改设备安装程序类的上限和下限的筛选器驱动程序
    -   添加和删除驱动程序存储区中的第三方驱动程序包
-   **重新启动设备或计算机**DevCon 可以重新启动本地设备、 重新启动按需、 在本地系统或重新启动本地系统，如果另一个 DevCon 操作所需的。

## <a name="span-iddevconsourcecodespanspan-iddevconsourcecodespanspan-iddevconsourcecodespandevcon-source-code"></a><span id="DevCon_source_code"></span><span id="devcon_source_code"></span><span id="DEVCON_SOURCE_CODE"></span>DevCon 源代码


DevCon 源代码也是可用的以便你可以检查 DevCon 用于检索和更改设置和配置数据的方法。 DevCon 演示如何使用[常规设置函数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))，[设备安装函数](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))，并[即插即用 Configuration Manager 功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。 源代码[设备控制台 (DevCon) 工具](https://go.microsoft.com/fwlink/p/?LinkId=617966)现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[DevCon 命令](devcon-general-commands.md)

[DevCon 示例](devcon-examples.md)

 

 






