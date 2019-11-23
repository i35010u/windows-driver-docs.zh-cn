---
title: 设备控制台 (DevCon.exe) 命令
description: DevCon （DevCon）是一个命令行工具，可在运行 Windows 的计算机上显示有关设备的详细信息。 你还可以使用 DevCon 来启用、禁用、安装、配置和删除设备。 DevCon 使用以下语法。
ms.assetid: b397c407-db1f-4e2a-8beb-4fe989bd06e0
keywords:
- 设备控制台（DevCon）命令驱动程序开发工具
topic_type:
- apiref
api_name:
- Device Console (DevCon.exe) Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc8a59d9e112b67109cf761e72b890e43405285c
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284910"
---
# <a name="device-console-devconexe-commands"></a>设备控制台 (DevCon.exe) 命令


DevCon （DevCon）是一个命令行工具，可在运行 Windows 的计算机上显示有关设备的详细信息。 你还可以使用 DevCon 来启用、禁用、安装、配置和删除设备。 DevCon 使用以下语法。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddk_devcon_general_commands_toolsspanspan-idddk_devcon_general_commands_toolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>Parameters


**注意**  要更改设备的状态或配置，您必须是计算机上 Administrators 组的成员。

 

DevCon 命令中的参数必须按语法中所示的顺序出现。 如果参数不按顺序排列，则 DevCon 将忽略这些参数，但不显示语法错误。 相反，它会处理包含剩余参数的命令。

有关命令语法的帮助，可以在命令提示符窗口中使用以下命令： **DevCon help**或**DevCon help** *命令*。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m：\\\\** <em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。
**请注意**   在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能不可用。

 

<span id="________r______"></span><span id="________R______"></span> **/r**条件重启。 仅当需要重新启动才能使更改生效时，才能在完成操作后重新启动系统。

此参数不同于[**DevCon reboot**](devcon-reboot.md)操作，该操作强制系统重新启动。 相反， **/r**参数根据随附操作的返回代码确定是否需要重新启动。有关详细信息，请参阅[重新启动和重新启动](#ddk-rebooting-and-restarting-tools)。

<span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*指定 DevCon 命令。 有关可用 DevCon 命令和命令参数的信息，请使用以下列表。

你还可以在命令提示符窗口中使用**DevCon help** *命令*获得语法帮助。

若要*列出和显示*有关计算机上的设备的信息，请使用以下命令：

[**DevCon Hwid**](devcon-hwids.md)

[**DevCon 类**](devcon-classes.md)

[**DevCon ListClass**](devcon-listclass.md)

[**DevCon DriverFiles**](devcon-driverfiles.md)

[**DevCon DriverNodes**](devcon-drivernodes.md)

[**DevCon 资源**](devcon-resources.md)

[**DevCon 堆栈**](devcon-stack.md)

[**DevCon 状态**](devcon-status.md)

[**DevCon Dp\_枚举**](devcon-dp-enum.md)

若要在计算机上*搜索*有关设备的信息，请使用以下命令：

[**DevCon 查找**](devcon-find.md)

[**DevCon FindAll**](devcon-findall.md)

若要操作设备或*更改*其配置，请使用以下命令：

[**DevCon 启用**](devcon-enable.md)

[**DevCon Disable**](devcon-disable.md)

[**DevCon 更新**](devcon-update.md)

[**DevCon UpdateNI**](devcon-updateni.md)

[**DevCon 安装**](devcon-install.md)

[**DevCon 删除**](devcon-remove.md)

[**DevCon 重新扫描**](devcon-rescan.md)

[**DevCon 重启**](devcon-restart.md)

[**DevCon 重新启动**](devcon-reboot.md)

[**DevCon SetHwID**](devcon-sethwid.md)

[**DevCon ClassFilter**](devcon-classfilter.md)

[**DevCon Dp\_添加**](devcon-dp-add.md)

[**删除 DevCon Dp\_** ](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span>*参数*指定 DevCon 命令的参数。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> **/?** 或 "**帮助**" 显示帮助。 如果指定操作，则 DevCon 会显示操作的详细帮助。

参数必须以指定的顺序出现。 例如，若要显示[**Devcon 状态**](devcon-status.md)操作的帮助，请键入**devcon/？ Status** （或**devcon help status**），而不是**devcon status/？** 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

许多 DevCon 操作都需要设备的硬件 ID。 若要创建计算机上的所有设备的硬件 Id 列表以在后续 DevCon 操作中使用，请从[**DevCon hwid**](devcon-hwids.md)命令开始。 有关详细信息，请参阅[硬件 id](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)和[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

### <a name="span-idddk_devcon_search_logic_toolsspanspan-idddk_devcon_search_logic_toolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>如何搜索设备

DevCon 按计算机名称、硬件 ID、兼容 ID、设备实例 ID 和/或设备安装程序类来标识设备。

如果命令包括多个 ID 或 ID 模式（一个包含通配符（\*）的 ID），则 DevCon 返回其 Id 与任何 Id 或 ID 模式匹配的设备。 也就是说，它在 ID 参数之间假定为 "or"。

例如， **devcon hwid \*pnp\* \*mou\*** 返回在其硬件 ID 或兼容 ID 中包含 "pnp" 或 "mou" 的设备。

如果命令包括设备安装程序类，则 DevCon 首先将搜索限制为安装类，然后返回类中与任何 ID 模式匹配的设备，也就是说，它在类和 Id 之间采用 "and"，在每个 ID 参数之间使用 "or"。

例如， **devcon hwid = media \*pnp\* \*microsoft\*** 返回 media 设备安装程序类中的设备，该设备在其硬件 ID 或兼容 ID 中包含 "pnp" 或 "microsoft"。

**请注意**   在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能不可用。

 

### <span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>重新启动和重新启动

DevCon 提供了两种方法来重新启动操作系统，还提供了一种方法来重新启动设备。

-   **/R**参数是仅当需要重新启动才能使随附的操作生效时才会重新启动操作系统的条件重启。 此参数仅在包含 DevCon 操作的命令中有效。 它可以在本地计算机或远程计算机（Windows XP 及更早版本）上重新启动系统。

-   **DevCon reboot**操作强制操作系统重启。 它仅在本地计算机上有效，不能与其他操作结合使用。 用户通常会将 **/r**参数添加到命令，而不是使用重新启动操作。

-   **DevCon Restart**操作重新启动指定的设备。 它仅在本地计算机上有效，不能与其他操作结合使用。

### <a name="span-idddk_devcon_return_codes_toolsspanspan-idddk_devcon_return_codes_toolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon 返回代码

DevCon 返回一个整数，该整数可在程序和脚本中用于确定 DevCon 命令是否成功（例如， **return = devcon hwid \*** ）。

下表列出并说明了返回代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>成功</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>需要重新启动</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>失败</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>语法错误</p></td>
</tr>
</tbody>
</table>

 

 

 





