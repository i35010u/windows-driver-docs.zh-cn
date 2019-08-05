---
title: 设备控制台 (DevCon.exe) 命令
description: DevCon (DevCon.exe) 是一个命令行工具，可以运行 Windows 的计算机上显示有关设备的详细的信息。 此外可以使用 DevCon 来启用、 禁用、 安装、 配置和删除设备。 DevCon 使用以下语法。
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
ms.localizationpriority: medium
ms.openlocfilehash: 092d6fd7be797f6529902525626d0f63f1c1ebd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371534"
---
# <a name="device-console-devconexe-commands"></a>设备控制台 (DevCon.exe) 命令


DevCon (DevCon.exe) 是一个命令行工具，可以运行 Windows 的计算机上显示有关设备的详细的信息。 此外可以使用 DevCon 来启用、 禁用、 安装、 配置和删除设备。 DevCon 使用以下语法。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddk_devcon_general_commands_toolsspanspan-idddk_devcon_general_commands_toolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>参数


**请注意**  若要更改的状态或设备的配置，必须是计算机上 Administrators 组的成员。

 

DevCon 命令中的参数必须出现在语法中所示的顺序。 如果参数不是按顺序，DevCon 会忽略它们，但不会显示语法错误。 相反，它可以处理剩余的参数的命令。

有关命令语法的帮助，可以在命令提示符窗口中使用以下命令：**DevCon 帮助**或**DevCon 帮助***命令*。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\** <em>计算机</em>指定远程计算机上运行该命令。 需要反斜杠。
**请注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和更高版本的 Windows 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能将不可用。

 

<span id="________r______"></span><span id="________R______"></span> **/r**条件重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

此参数不同于[ **DevCon 重启**](devcon-reboot.md)操作，这会强制系统重新启动。 相反， **/r**参数确定是否必须重新启动，基于随附的操作的返回代码。有关详细信息，请参阅[正在重启并重新启动](#ddk-rebooting-and-restarting-tools)。

<span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*指定 DevCon 命令。 有关可用 DevCon 命令和命令参数的信息，请使用下面的列表。

此外可以获取在命令提示符窗口中使用的语法帮助**DevCon 帮助***命令*。

向*列出并显示*设备信息的计算机上，使用以下命令：

[**DevCon HwIDs**](devcon-hwids.md)

[**DevCon 类**](devcon-classes.md)

[**DevCon ListClass**](devcon-listclass.md)

[**DevCon DriverFiles**](devcon-driverfiles.md)

[**DevCon DriverNodes**](devcon-drivernodes.md)

[**DevCon 资源**](devcon-resources.md)

[**DevCon Stack**](devcon-stack.md)

[**DevCon Status**](devcon-status.md)

[**DevCon Dp\_枚举**](devcon-dp-enum.md)

向*搜索*有关设备的计算机上的信息，请使用以下命令：

[**DevCon 查找**](devcon-find.md)

[**DevCon FindAll**](devcon-findall.md)

处理设备或*更改*其配置中，使用以下命令：

[**DevCon 启用**](devcon-enable.md)

[**DevCon 禁用**](devcon-disable.md)

[**DevCon 更新**](devcon-update.md)

[**DevCon UpdateNI**](devcon-updateni.md)

[**DevCon 安装**](devcon-install.md)

[**DevCon Remove**](devcon-remove.md)

[**DevCon 重新扫描**](devcon-rescan.md)

[**DevCon 重新启动**](devcon-restart.md)

[**DevCon Reboot**](devcon-reboot.md)

[**DevCon SetHwID**](devcon-sethwid.md)

[**DevCon ClassFilter**](devcon-classfilter.md)

[**DevCon Dp\_添加**](devcon-dp-add.md)

[**DevCon Dp\_删除**](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *参数*DevCon 命令自变量。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> **/?** 或**帮助**显示帮助。 如果指定一个操作，DevCon 显示有关该操作的详细的帮助。

参数必须出现在指定的顺序。 例如，若要显示的帮助[ **DevCon 状态**](devcon-status.md)操作中，键入**devcon /？ 状态**(或**devcon 帮助状态**)，而非**devcon 状态 /？** .

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

许多 DevCon 操作需要的设备硬件 ID。 若要在后续 DevCon 操作中使用计算机上创建的所有设备 Id 的硬件的列表，以开头[ **DevCon HwIDs** ](devcon-hwids.md)命令。 有关详细信息，请参阅[硬件 Id](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)并[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

### <a name="span-idddk_devcon_search_logic_toolsspanspan-idddk_devcon_search_logic_toolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>DevCon 搜索设备的方式

DevCon 标识其计算机名称、 硬件 ID、 兼容 ID、 设备实例 ID 和/或设备安装程序类的设备。

如果命令包含多个 ID 或 ID 模式 (包含通配符字符的 ID (\*))，DevCon 返回其 Id 与匹配的设备 Id 或 ID 模式。 也就是说，它假定"所得的 ID 参数。

例如， **devcon hwids \*pnp\* \*mou\\** * 返回包含"pnp"或"mou"的设备在其硬件 ID 或兼容 id。

如果命令包含设备安装程序类，DevCon 首次将搜索限定为安装程序类，然后返回与任何 ID 模式匹配的类中的设备，即，假定"和"类和 Id 和"每个 ID 自变量之间。

例如， **devcon hwids = 媒体\*pnp\* \*microsoft\\** * 返回其硬件 ID 中的设备中包括的媒体设备安装程序类"pnp"或"microsoft"或兼容 id。

**请注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和更高版本的 Windows 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问功能将不可用。

 

### <span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>重新启动并重新启动

DevCon 提供两种方法来重新启动操作系统和重启设备的一种方法。

-   **/R**参数是在重新启动操作系统，仅当需要重新启动以使随附操作生效的条件性重新启动。 此参数是仅在包含 DevCon 操作的命令中有效。 它可以重新启动本地计算机或远程计算机上的系统 (Windows XP 及更早版本)。

-   **DevCon 重启**操作强制重新启动的操作系统。 它仅在本地计算机上有效且不能结合其他操作。 而不是使用重启操作，用户通常添加 **/r**命令的参数。

-   **DevCon 重启**操作重新启动指定的设备。 它仅在本地计算机上有效且不能结合其他操作。

### <a name="span-idddk_devcon_return_codes_toolsspanspan-idddk_devcon_return_codes_toolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon 返回代码

DevCon 程序和脚本以确定是否成功 DevCon 命令中返回一个整数，可使用 (例如，* * 返回 = devcon hwids \\* * *)。

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

 

 

 





