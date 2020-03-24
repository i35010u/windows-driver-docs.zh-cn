---
title: Windows 设备控制台 (Devcon.exe)
description: DevCon (Devcon.exe)（即设备控制台）是一种命令行工具，用于显示有关运行 Windows 的计算机上的设备的详细信息。
ms.assetid: ac74200e-e2ae-40db-9fb7-5ea2e7760613
keywords:
- DevCon WDK
- 设备控制台 WDK
- 驱动程序测试 WDK、DevCon
- 测试驱动程序 WDK、DevCon
- 设备信息 WDK DevCon
- 搜索 WDK DevCon
- 显示设备信息
- 更改设备配置 WDK DevCon
- 操作设备 WDK DevCon
- 状态更改 WDK DevCon
- 正在重启设备
- 设备管理 WDK DevCon
- 列出设备信息 WDK
ms.date: 04/20/2017
ms.localizationpriority: high
ms.openlocfilehash: d5c3e1418e05d8ffc0a852d626dbefbe1433dc72
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335943"
---
# <a name="windows-device-console-devconexe"></a>Windows 设备控制台 (Devcon.exe)


DevCon (Devcon.exe)（即设备控制台）是一种命令行工具，用于显示有关运行 Windows 的计算机上的设备的详细信息。 可以使用 DevCon 启用、禁用、安装、配置以及删除设备。

DevCon 在 Microsoft Windows 2000 和更高版本的 Windows 上运行。

## <span id="ddk_devcon_tools"></span><span id="DDK_DEVCON_TOOLS"></span>


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以下载 DevCon？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>安装适用于桌面应用的 WDK、Visual Studio 和 Windows SDK 时，DevCon (Devcon.exe) 会包括在内。 有关下载工具包的信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包 (WDK) 8 和 Windows 驱动程序工具包 (WDK) 8.1</strong>（安装路径）</p>
<p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p>
<p>%WindowsSdkDir%\tools\arm\devcon.exe</p>
<div class="alert">
<strong>注意</strong>  Visual Studio 环境变量（%WindowsSdkDir%）表示安装了工具包的 Windows 工具包目录的路径，例如 C:\Program Files (x86)\Windows Kits\8.1。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

本部分包括：

[DevCon 命令](devcon-general-commands.md)

[DevCon 示例](devcon-examples.md)

## <a name="span-idwhat_you_can_do_with_devconspanspan-idwhat_you_can_do_with_devconspanspan-idwhat_you_can_do_with_devconspanwhat-you-can-do-with-devcon"></a><span id="What_you_can_do_with_DevCon"></span><span id="what_you_can_do_with_devcon"></span><span id="WHAT_YOU_CAN_DO_WITH_DEVCON"></span>可以利用 DevCon 执行的操作


Windows 驱动程序开发人员和测试人员可以使用 DevCon 验证是否已正确安装和配置了驱动程序，包括正确的 INF 文件、驱动程序堆栈、驱动程序文件和驱动程序包。 你还可以在脚本中使用 DevCon 命令（启用、禁用、安装、启动、停止和继续）来测试驱动程序。

DevCon 是一种命令行工具，可在本地计算机和远程计算机上执行设备管理功能。

**注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。

 

Devcon 的功能包括：

-   **显示驱动程序和设备信息** DevCon 可以显示本地计算机和远程计算机（运行 Windows XP 及更低版本）上的驱动程序和设备的以下属性：
    -   硬件 ID、兼容 ID 和设备实例 ID。 有关这些标识符的详细信息，请参阅[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。
    -   [设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)
    -   设备安装程序类中的设备
    -   INF 文件和设备驱动程序文件
    -   [驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)的详细信息
    -   硬件资源
    -   设备状态
    -   需要的驱动程序堆栈
    -   驱动程序存储中的第三方驱动程序包
-   **搜索设备** DevCon 可以通过硬件 ID、设备实例 ID 或设备安装程序类搜索本地或远程计算机上已安装和已卸载的设备。

-   **更改设备设置** DevCon 可以通过以下方式更改本地计算机上即插即用 (PnP) 设备的状态或配置：
    -   启用设备
    -   禁用设备
    -   更新驱动程序（交互式和非交互式）
    -   安装设备（创建 devnode 并安装软件）
    -   从设备树中删除设备，并删除其设备堆栈
    -   重新扫描即插即用设备
    -   添加、删除根枚举设备的硬件 ID 并对其进行重新排列
    -   更改设备安装程序类的上层和下层筛选器驱动程序
    -   从驱动程序存储中添加和删除第三方驱动程序包
-   **重启设备或计算机** DevCon 可以重启本地设备、按需重启本地系统，或在其他 DevCon 操作需要时重启本地系统。

## <a name="span-iddevcon_source_codespanspan-iddevcon_source_codespanspan-iddevcon_source_codespandevcon-source-code"></a><span id="DevCon_source_code"></span><span id="devcon_source_code"></span><span id="DEVCON_SOURCE_CODE"></span>DevCon 源代码


还可以使用 DevCon 源代码，以便查看 DevCon 用于检索安装程序和配置数据并对其进行更改的方法。 DevCon 说明了如何使用[常规安装程序功能](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))、[设备安装程序功能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))和 [PnP Configuration Manager 功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。 GitHub 上的 [Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中提供了[设备控制台 (DevCon)](https://go.microsoft.com/fwlink/p/?LinkId=617966) 工具的源代码。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[DevCon 命令](devcon-general-commands.md)

[DevCon 示例](devcon-examples.md)

 

 






