---
title: 设备控制台 (DevCon.exe) 命令
description: DevCon (DevCon.exe) 是一种命令行工具，用于显示有关运行 Windows 的计算机上的设备的详细信息。 你也可以使用 DevCon 启用、禁用、安装、配置以及删除设备。 DevCon 使用以下语法。
ms.assetid: b397c407-db1f-4e2a-8beb-4fe989bd06e0
keywords:
- 设备控制台 (DevCon.exe) 命令驱动程序开发工具
topic_type:
- apiref
api_name:
- Device Console (DevCon.exe) Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: high
ms.openlocfilehash: aeff1990d5695440e0f7431334f26e7782863027
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335945"
---
# <a name="device-console-devconexe-commands"></a>设备控制台 (DevCon.exe) 命令


DevCon (DevCon.exe) 是一种命令行工具，用于显示有关运行 Windows 的计算机上的设备的详细信息。 你也可以使用 DevCon 启用、禁用、安装、配置以及删除设备。 DevCon 使用以下语法。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddk_devcon_general_commands_toolsspanspan-idddk_devcon_general_commands_toolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>参数


**注意**  若要更改设备的状态或配置，你必须是计算机上 Administrators 组的成员。

 

DevCon 命令中的参数必须按照语法中显示的顺序显示。 如果参数不按顺序显示，则 DevCon 将忽略这些参数，但不显示语法错误。 而是使用其余参数处理命令。

要获得有关命令语法方面的帮助，可以在“命令提示符”窗口中使用以下命令：DevCon help 或 DevCon help 命令    。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> /m:\\\\<em>computer</em>  在指定的远程计算机上运行该命令。 必须使用反斜杠。
**注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能不可用。

 

<span id="________r______"></span><span id="________R______"></span> /r  条件重启。 仅当需要重启才能使更改生效时，才能在完成操作后重启系统。

此参数与 [DevCon Reboot](devcon-reboot.md) 操作不同，后者强制系统重启  。 相反，/r  参数根据伴随操作的返回代码确定是否需要重启。有关详细信息，请参阅[重启](#ddk-rebooting-and-restarting-tools)。

<span id="_______command______"></span><span id="_______COMMAND______"></span> 命令  指定 DevCon 命令。 有关可用的 DevCon 命令和命令参数的信息，请使用以下列表。

还可以使用 DevCon help 命令在“命令提示符”窗口中获取语法帮助   。

若要列出和显示有关计算机上设备的信息，请使用以下命令  ：

[DevCon HwIDs  ](devcon-hwids.md)

[DevCon Classes  ](devcon-classes.md)

[DevCon ListClass  ](devcon-listclass.md)

[DevCon DriverFiles  ](devcon-driverfiles.md)

[DevCon DriverNodes  ](devcon-drivernodes.md)

[DevCon Resources  ](devcon-resources.md)

[DevCon Stack  ](devcon-stack.md)

[DevCon Status  ](devcon-status.md)

[DevCon Dp\_enum  ](devcon-dp-enum.md)

若要搜索有关计算机上设备的信息，请使用以下命令  ：

[DevCon Find  ](devcon-find.md)

[DevCon FindAll  ](devcon-findall.md)

若要操作设备或更改其配置，请使用以下命令  ：

[DevCon Enable  ](devcon-enable.md)

[DevCon Disable  ](devcon-disable.md)

[DevCon Update  ](devcon-update.md)

[DevCon UpdateNI  ](devcon-updateni.md)

[DevCon Install  ](devcon-install.md)

[DevCon Remove  ](devcon-remove.md)

[DevCon Rescan  ](devcon-rescan.md)

[DevCon Restart  ](devcon-restart.md)

[DevCon Reboot  ](devcon-reboot.md)

[DevCon SetHwID  ](devcon-sethwid.md)

[DevCon ClassFilter  ](devcon-classfilter.md)

[DevCon Dp\_add  ](devcon-dp-add.md)

[DevCon Dp\_delete  ](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> 参数  指定 DevCon 命令的参数。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> /?  或 help  显示帮助。 如果指定操作，DevCon 会显示该操作的详细帮助。

参数必须以指定的顺序出现。 例如，若要显示 [DevCon Status](devcon-status.md) 操作的帮助，请键入“devcon /? status”（或 devcon help status），而不是键入“devcon status /?”     。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>备注

许多 DevCon 操作都需要设备的硬件 ID。 若要创建计算机上的所有设备的硬件 ID 列表，以用于后续的 DevCon 操作，请从 [DevCon HwIDs  ](devcon-hwids.md) 命令开始。 有关详细信息，请参阅[硬件 ID](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids) 和[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

### <a name="span-idddk_devcon_search_logic_toolsspanspan-idddk_devcon_search_logic_toolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>DevCon 如何搜索设备

DevCon 通过计算机名称、硬件 ID、兼容 ID、设备实例 ID 和/或设备安装程序类来标识设备。

如果命令包含多个 ID 或 ID 模式（一个包含通配符 (\*) 的 ID），DevCon 将返回其 ID 与任何 ID 或 ID 模式都匹配的设备。 也就是说，它假定 ID 参数之间为“or”的关系。

例如，devcon hwids \*pnp\* \*mou\*  返回在其硬件 ID 或兼容 ID 中包含“pnp”或“mou”的设备。

如果命令包含设备安装程序类，则 DevCon 首先会将搜索限制为安装程序类，然后返回类中与任何 ID 模式匹配的设备，也就是说，它假定在类和 ID 之间存在“and”关系，而在每个 ID 参数之间存在“or”关系。

例如，devcon hwids =media \*pnp\* \*microsoft\*  返回媒体设备安装程序类中的设备，这些设备在其硬件 ID 或兼容 ID 中包含“pnp”或“microsoft”。

**注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能不可用。

 

### <a name="span-idddk_rebooting_and_restarting_toolsspanspan-idddk_rebooting_and_restarting_toolsspanrebooting-and-restarting"></a><span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>重启

DevCon 提供了两种重启操作系统的方法和一种重启设备的方法。

-   /r 参数是一个条件重启，它仅在需要重启才能使随附的操作生效时才会重启操作系统  。 此参数仅在包含 DevCon 操作的命令中有效。 它可以在本地计算机或远程计算机（Windows XP 及更低版本）上重启系统。

-   DevCon Reboot 操作强制操作系统重启  。 它仅在本地计算机上有效，不能与其他操作结合使用。 用户通常不使用重启操作，而是将 /r 参数添加到命令中  。

-   DevCon Restart 操作重启指定的设备  。 它仅在本地计算机上有效，不能与其他操作结合使用。

### <a name="span-idddk_devcon_return_codes_toolsspanspan-idddk_devcon_return_codes_toolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon 返回代码

DevCon 返回一个整数，可在程序和脚本中使用该整数来确定 DevCon 命令是否成功（例如 return = devcon hwids \*  ）。

下表列出并描述了返回代码。

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
<td align="left"><p>需要重启</p></td>
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

 

 

 





